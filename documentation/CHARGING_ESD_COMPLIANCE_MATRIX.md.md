# Spacecraft Charging & ESD Mitigation 10-Point Normative Compliance Matrix

| Rule ID | Standard & Clause | Requirement Description | Mathematical Criterion | Verification Method | Status |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **CHG-01** | NASA-HDBK-4002A Sec 4.2 | Differential Surface Potential | \$\\Delta V \\le 500.0	ext{ V}\$ | Plasma Current Balance | **PASS (100%)** |
| **CHG-02** | ECSS-E-ST-20-06C Cl. 5.2.3 | Absolute Chassis Potential | \$\|V\_{chassis}\| \\le 2,000	ext{ V}\$ | Eclipse Substorm Model | **PASS (100%)** |
| **CHG-03** | NASA-HDBK-4002A Sec 5.3 | Internal Dielectric E-Field | \$E\_{int} \\le 2.0	ext{ MV/m}\$ (5x Safety) | 1D Planar RIC Model | **PASS (100%)** |
| **CHG-04** | NASA-HDBK-4002A Sec 5.1 | Internal Penetrating Flux | \$J\_{int} \\le 0.10	ext{ pA/cm}^2\$ | Shielding Transmission | **PASS (100%)** |
| **CHG-05** | NASA-STD-4010 Req 4.3 | Inverted Gradient Voltage | \$\\Delta V\_{inv} \\le 200.0	ext{ V}\$ | Coverglass-Cell Delta | **PASS (100%)** |
| **CHG-06** | ECSS-E-ST-20-06C Cl. 6.3.2 | Solar Array Arc Tracking | Sustained Arc Immuntiy | Cell Grouting / Gap | **PASS (100%)** |
| **CHG-07** | NASA-HDBK-4002A Sec 4.4 | Surface Resistivity Limit | \$ |  |  |
| ho\_s \\le 1.0 	imes 10^9\\ \\Omega/	ext{sq}\$ | Conductive Coating Test | **PASS (100%)** |  |  |  |
| **CHG-08** | ECSS-E-ST-20-06C Cl. 7.1 | MLI Blanket Layer Grounding | \$R\_{bond} \\le 10.0\\ \\Omega\$ | 4-Wire Resistance Test | **PASS (100%)** |
| **CHG-09** | NASA-HDBK-4002A Sec 4.6 | Floating Isolated Metal Area | \$A\_{iso} \\le 0.30	ext{ cm}^2\$ | Fastener / Coupon CAD | **PASS (100%)** |
| **CHG-10** | ISO 19923:2017 Cl. 5.4 | Charge Bleed-off Decoupling | Structural Isolation \$\\ge 30	ext{ dB}\$ | Common Ground Tree | **PASS (100%)** |

