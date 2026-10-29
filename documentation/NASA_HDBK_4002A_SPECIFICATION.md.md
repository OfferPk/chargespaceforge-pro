# NASA-HDBK-4002A & ECSS-E-ST-20-06C Spacecraft Charging & ESD Mitigation Specification

## 1\. Executive Engineering Overview

ChargeSpaceForge Pro v1.0.0 implements the complete spacecraft surface and internal deep dielectric electrostatic charging engineering standards per:

- **NASA-HDBK-4002A**: *Mitigating In-Space Charging Effects—A Guideline*  
- **ECSS-E-ST-20-06C**: *Space Engineering — Spacecraft Charging*  
- **NASA-STD-4010**: *Mitigating In-Space Charging Effects*  
- **ISO 19923:2017**: *Space Systems — Spacecraft Charging Prevention and Mitigation*

## 2\. Core Electromagnetic & Plasma Interaction Domains

### 2.1 Surface Charging in GEO Substorms & Auroral LEO

- Ambient plasma electron temperature: \$T\_e \= 1	ext{ to }25	ext{ keV}\$  
- Ambient plasma electron density: \$n\_e \= 0.2	ext{ to }20.0	ext{ cm}^{-3}\$  
- Current balance equilibrium: \$\$J\_{net}(V) \= J\_e(V) \- J\_i(V) \- J\_{se}(V) \- J\_{si}(V) \- J\_{ph}(V) \= 0\$\$  
- In eclipse, photoemission drops to zero (\$J\_{ph0} \= 0\$), causing negative potential build-up.  
- Differential Surface Potential Envelope: \$\\Delta V \= \|V\_{surface} \- V\_{chassis}\| \\le 500.0	ext{ V}\$ per NASA-HDBK-4002A Section 4.2.  
- Absolute Chassis Ground Potential: \$\|V\_{chassis}\| \\le 2,000.0	ext{ V}\$ per ECSS-E-ST-20-06C Clause 5.2.3.

### 2.2 Deep Dielectric Internal Charging

- Penetrating relativistic "killer electron" flux (\$E \> 1.0	ext{ MeV}\$) through aluminum chassis walls (\$t\_{shield} \= 0.5	ext{ to }3.0	ext{ mm}\$).  
- Internal current density ceiling behind shielding: \$J\_{int} \\le 0.10	ext{ pA/cm}^2\$ (\$10^{-9}	ext{ A/m}^2\$) per NASA Section 5.3.  
- Steady-state electric field buildup: \$\$E\_{int} \= J\_{int} \\cdot ho\_{bulk} \\cdot 	ext{RIC}(E)\$\$  
- Critical dielectric breakdown threshold: \$E\_{breakdown} \= 1.0 	imes 10^7	ext{ V/m}\$ (\$100	ext{ kV/cm}\$).  
- Mandatory 5x Safety Factor Design Limit: \$E\_{int} \\le 2.0 	imes 10^6	ext{ V/m}\$ (\$20	ext{ kV/cm}\$, margin \$\\ge \+14.0	ext{ dB}\$).

### 2.3 Solar Array Inverted-Potential Gradient ESD & Sustained Arcing

- When solar cell interconnects are positive relative to coverglasses (\$V\_{cell} \- V\_{coverglass} \> 200	ext{ V}\$), electron flashover sparks trigger primary discharges.  
- High-voltage bus arcs (\$V\_{bus} \\ge 50	ext{ V to }100	ext{ V}\$) can transition from temporary ESD sparks into sustained secondary plasma short-circuit arcs that vaporize silver inter-cell interconnects.  
- Mitigation: Conductive ITO coverglasses grounded to chassis, inter-cell spacing \$\\ge 1.0	ext{ mm}\$ or RTV silicone grouting.

### 2.4 Grounding & Bleed-off Rules

- Maximum static dissipative surface resistivity: \$ ho\_s \\le 1.0 	imes 10^9\\ \\Omega/	ext{sq}\$ per NASA-HDBK-4002A Section 4.4.  
- Multi-Layer Insulation (MLI) grounding: All metallized Kapton/Mylar layers bonded to chassis with \$R\_{bond} \\le 10.0\\ \\Omega\$ per layer.  
- Ungrounded floating metallic coupon area: \$A\_{iso} \\le 0.30	ext{ cm}^2\$ per NASA-HDBK-4002A Section 4.6.