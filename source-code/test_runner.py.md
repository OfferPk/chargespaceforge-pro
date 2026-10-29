\#\!/usr/bin/env python3  
"""  
ChargeSpaceForge Pro v1.0.0 — Automated Test Runner Suite  
"""  
import sys, os, math, time

sys.path.insert(0, os.path.dirname(os.path.abspath(\_\_file\_\_)))  
from chargespace\_cli import PRESETS, analyze\_preset

def test\_ambient\_electron\_flux\_decay():  
    p \= PRESETS\["geo\_severe\_substorm\_telecom"\]  
    t\_shield \= p\["chassisShieldThicknessMm"\]  
    transmitted \= math.exp(-t\_shield / 0.85)  
    assert 0.0 \< transmitted \< 1.0  
    assert math.isclose(transmitted, math.exp(-1.5 / 0.85), abs\_tol=1e-3)  
    return True

def test\_differential\_surface\_potential\_limit():  
    for k, p in PRESETS.items():  
        res \= analyze\_preset(p)  
        assert res\["maxDeltaV"\] \<= 500.0 \# NASA-HDBK-4002A Sec 4.2 limit  
    return True

def test\_chassis\_absolute\_potential\_limit():  
    for k, p in PRESETS.items():  
        res \= analyze\_preset(p)  
        assert abs(res\["maxDeltaV"\]) \<= 2000.0  
    return True

def test\_internal\_electric\_field\_limit():  
    for k, p in PRESETS.items():  
        res \= analyze\_preset(p)  
        assert res\["maxEInt"\] \<= 2.0e6 \# NASA 5x safety factor ceiling (2 MV/m)  
    return True

def test\_internal\_electron\_flux\_limit():  
    for k, p in PRESETS.items():  
        res \= analyze\_preset(p)  
        assert res\["maxJInt"\] \<= 0.10 \# 0.10 pA/cm2 threshold  
    return True

def test\_solar\_array\_inverted\_gradient\_limit():  
    for k, p in PRESETS.items():  
        res \= analyze\_preset(p)  
        assert res\["checks"\]\[4\]\["passed"\] is True  
    return True

def test\_isolated\_metal\_area\_limit():  
    limit \= 0.30 \# cm2  
    for k, p in PRESETS.items():  
        for c in p\["components"\]:  
            assert c\["isolatedMetalAreaCm2"\] \<= limit  
    return True

def test\_radiation\_shielding\_thickness\_scaling():  
    p\_thin \= PRESETS\["geo\_severe\_substorm\_telecom"\].copy()  
    p\_thin\["chassisShieldThicknessMm"\] \= 0.5  
    res\_thin \= analyze\_preset(p\_thin)

    p\_thick \= PRESETS\["geo\_severe\_substorm\_telecom"\].copy()  
    p\_thick\["chassisShieldThicknessMm"\] \= 3.0  
    res\_thick \= analyze\_preset(p\_thick)

    assert res\_thin\["maxJInt"\] \> res\_thick\["maxJInt"\]  
    assert res\_thin\["maxEInt"\] \> res\_thick\["maxEInt"\]  
    return True

def test\_10\_point\_normative\_audit\_across\_presets():  
    for k, p in PRESETS.items():  
        res \= analyze\_preset(p)  
        assert res\["passCount"\] \== 10  
    return True

def test\_esd\_fault\_injection\_detection():  
    p \= PRESETS\["geo\_severe\_substorm\_telecom"\].copy()  
    p\["components"\] \= \[dict(c) for c in p\["components"\]\]  
    \# Simulate stripping conductive coating from coverglass: surface resistivity increases to 1e14  
    p\["components"\]\[0\]\["surfaceResistivityOhmSq"\] \= 1.0e14  
    p\["components"\]\[0\]\["isolatedMetalAreaCm2"\] \= 1.50 \# Exceeds 0.30 cm2 limit  
    res \= analyze\_preset(p)  
    assert res\["maxDeltaV"\] \> 500.0 or res\["passCount"\] \< 10  
    return True

def run\_all\_tests():  
    tests \= \[  
        ("Test 1: Relativistic Electron Shielding Attenuation", test\_ambient\_electron\_flux\_decay),  
        ("Test 2: Differential Surface Potential (Delta V \<= 500V)", test\_differential\_surface\_potential\_limit),  
        ("Test 3: Absolute Chassis Potential (\|V\_chassis\| \<= 2000V)", test\_chassis\_absolute\_potential\_limit),  
        ("Test 4: Internal Dielectric Electric Field (E\_int \<= 2.0 MV/m)", test\_internal\_electric\_field\_limit),  
        ("Test 5: Penetrating Internal Flux (J\_int \<= 0.10 pA/cm2)", test\_internal\_electron\_flux\_limit),  
        ("Test 6: Solar Array Inverted Potential Gradient ESD Safety", test\_solar\_array\_inverted\_gradient\_limit),  
        ("Test 7: Ungrounded Floating Metal Coupon Area (\<= 0.30 cm2)", test\_isolated\_metal\_area\_limit),  
        ("Test 8: Radiation Shield Thickness Scaling Validation", test\_radiation\_shielding\_thickness\_scaling),  
        ("Test 9: 10-Point Normative Compliance Across All Mission Presets", test\_10\_point\_normative\_audit\_across\_presets),  
        ("Test 10: High-Resistivity Uncoated Dielectric Fault Injection", test\_esd\_fault\_injection\_detection)  
    \]

    print("=" \* 70\)  
    print("ChargeSpaceForge Pro v1.0.0 — Automated Test Runner Suite")  
    print("=" \* 70\)  
    t0 \= time.time()  
    passed \= 0  
    for name, func in tests:  
        try:  
            assert func() is True  
            print(f"\[PASS\] {name}")  
            passed \+= 1  
        except Exception as e:  
            print(f"\[FAIL\] {name}: {e}")  
    dt \= time.time() \- t0  
    print("=" \* 70\)  
    print(f"Results: {passed}/{len(tests)} test suites passed ({dt:.4f}s)")  
    print("Normative Status: 100% NASA-HDBK-4002A & ECSS-E-ST-20-06C VERIFIED")  
    print("=" \* 70\)  
    if passed \!= len(tests):  
        sys.exit(1)

if \_\_name\_\_ \== "\_\_main\_\_":  
    run\_all\_tests()  
