/\*\*  
 \* ChargeSpaceForge Pro v1.0.0 — Spacecraft Charging & ESD Physics Engine  
 \* Standards: NASA-HDBK-4002A, ECSS-E-ST-20-06C, NASA-STD-4010, ISO 19923  
 \* Pure ES6 Zero-Dependency Module  
 \*/

export const CHARGESPACE\_CONSTANTS \= {  
  ELEMENTARY\_CHARGE\_C: 1.602176634e-19,  
  ELECTRON\_MASS\_KG: 9.1093837e-31,  
  PROTON\_MASS\_KG: 1.6726219e-27,  
  EPSILON\_0\_F\_PER\_M: 8.8541878128e-12,  
  PHOTOELECTRON\_FLUX\_AM0\_A\_PER\_M2: 30.0e-6, // \~30 uA/m2 in direct 1 AU sunlight  
  MAX\_ALLOWABLE\_DIFF\_POTENTIAL\_V: 500.0,    // NASA-HDBK-4002A Sec 4.2 differential surface limit (V)  
  MAX\_ALLOWABLE\_CHASSIS\_POTENTIAL\_V: 2000.0,// ECSS-E-ST-20-06C chassis absolute limit in eclipse (V)  
  DIELECTRIC\_BREAKDOWN\_FIELD\_V\_PER\_M: 1.0e7,// 10 MV/m (100 kV/cm or 10 V/um) standard breakdown  
  MAX\_DESIGN\_ELECTRIC\_FIELD\_V\_PER\_M: 2.0e6, // NASA-HDBK-4002A 5x safety factor limit (2 MV/m)  
  MAX\_INTERNAL\_CURRENT\_DENSITY\_PA\_CM2: 0.10,// NASA Section 5.3 deep dielectric flux ceiling (0.1 pA/cm2)  
  MAX\_SURFACE\_RESISTIVITY\_OHM\_SQ: 1.0e9,    // Static dissipative surface ceiling (1 Giga-ohm/sq)  
  MAX\_ISOLATED\_METAL\_AREA\_CM2: 0.30         // Maximum allowable ungrounded metal coupon area (cm2)  
};

export const CHARGESPACE\_PRESETS \= {  
  geo\_severe\_substorm\_telecom: {  
    id: "geo\_severe\_substorm\_telecom",  
    name: "4,500 kg High-Throughput GEO Communications Satellite (100V Bus, Severe Midnight Substorm)",  
    orbitRegime: "GEO 35,786 km (Midnight Sector)",  
    sunlightCondition: "eclipse", // Worst case for surface charging  
    plasmaElectronTempKev: 12.0,  
    plasmaElectronDensityCm3: 1.2,  
    plasmaIonTempKev: 18.0,  
    plasmaIonDensityCm3: 1.2,  
    killerElectronFluxMev: 2.5e4, // electrons / (cm2\*s\*sr) at E \> 1 MeV  
    chassisShieldThicknessMm: 1.5, // Aluminum equivalent  
    busVoltageV: 100.0,  
    hasActiveChargeMitigation: false,  
    components: \[  
      { id: "MAT-01", name: "Solar Array Coverglass (Fused Silica \+ Conductive ITO)", type: "solar\_coverglass", bulkResistivityOhmM: 1.0e12, relPermittivity: 3.8, thicknessMm: 0.15, surfaceResistivityOhmSq: 5.0e6, capacitancePfCm2: 22.4, isolatedMetalAreaCm2: 0.05, grounded: true },  
      { id: "MAT-02", name: "Thermal MLI Outer Cover (Black Kapton, Carbon-Filled)", type: "thermal\_blanket", bulkResistivityOhmM: 1.0e9, relPermittivity: 3.4, thicknessMm: 0.05, surfaceResistivityOhmSq: 8.0e5, capacitancePfCm2: 60.2, isolatedMetalAreaCm2: 0.10, grounded: true },  
      { id: "MAT-03", name: "Internal Avionics FR4 Multilayer PCB", type: "internal\_pcb", bulkResistivityOhmM: 5.0e13, relPermittivity: 4.4, thicknessMm: 1.60, surfaceResistivityOhmSq: 1.0e12, capacitancePfCm2: 2.4, isolatedMetalAreaCm2: 0.02, grounded: true },  
      { id: "MAT-04", name: "High-Voltage Power Harness FEP Teflon Dielectric", type: "cable\_insulation", bulkResistivityOhmM: 1.0e16, relPermittivity: 2.1, thicknessMm: 0.80, surfaceResistivityOhmSq: 1.0e15, capacitancePfCm2: 2.3, isolatedMetalAreaCm2: 0.00, grounded: true },  
      { id: "MAT-05", name: "Optical Second Surface Mirror (Silvered Quartz OSR)", type: "radiator\_mirror", bulkResistivityOhmM: 2.0e12, relPermittivity: 3.8, thicknessMm: 0.20, surfaceResistivityOhmSq: 2.0e7, capacitancePfCm2: 16.8, isolatedMetalAreaCm2: 0.08, grounded: true }  
    \]  
  },  
  polar\_leo\_auroral\_imaging: {  
    id: "polar\_leo\_auroral\_imaging",  
    name: "350 kg LEO Optical Remote Sensing Satellite (28V Bus, 800 km SSO Auroral Inverted-V)",  
    orbitRegime: "Polar LEO 800 km (Auroral Zone)",  
    sunlightCondition: "sunlit",  
    plasmaElectronTempKev: 5.0,  
    plasmaElectronDensityCm3: 8.0,  
    plasmaIonTempKev: 2.0,  
    plasmaIonDensityCm3: 8.0,  
    killerElectronFluxMev: 8.0e3,  
    chassisShieldThicknessMm: 1.2,  
    busVoltageV: 28.0,  
    hasActiveChargeMitigation: false,  
    components: \[  
      { id: "MAT-01", name: "Solar Array Coverglass (Ceria-Doped Microsheet)", type: "solar\_coverglass", bulkResistivityOhmM: 2.0e12, relPermittivity: 3.8, thicknessMm: 0.10, surfaceResistivityOhmSq: 1.0e7, capacitancePfCm2: 33.6, isolatedMetalAreaCm2: 0.04, grounded: true },  
      { id: "MAT-02", name: "Telescope Carbon-Fiber Composite Sunshade Shell", type: "thermal\_blanket", bulkResistivityOhmM: 1.0e4, relPermittivity: 2.5, thicknessMm: 1.20, surfaceResistivityOhmSq: 2.0e3, capacitancePfCm2: 1.8, isolatedMetalAreaCm2: 0.00, grounded: true },  
      { id: "MAT-03", name: "Focal Plane Array Flexible Polyimide Harness", type: "cable\_insulation", bulkResistivityOhmM: 2.0e14, relPermittivity: 3.4, thicknessMm: 0.12, surfaceResistivityOhmSq: 1.0e13, capacitancePfCm2: 25.1, isolatedMetalAreaCm2: 0.01, grounded: true },  
      { id: "MAT-04", name: "Star Tracker Baffle Anodized Aluminum Bracket", type: "structural\_bracket", bulkResistivityOhmM: 1.0e10, relPermittivity: 8.5, thicknessMm: 0.02, surfaceResistivityOhmSq: 5.0e8, capacitancePfCm2: 376.0, isolatedMetalAreaCm2: 0.12, grounded: true },  
      { id: "MAT-05", name: "S-Band Patch Antenna Dielectric Substrate (PTFE)", type: "internal\_pcb", bulkResistivityOhmM: 1.0e15, relPermittivity: 2.2, thicknessMm: 1.50, surfaceResistivityOhmSq: 1.0e14, capacitancePfCm2: 1.3, isolatedMetalAreaCm2: 0.00, grounded: true }  
    \]  
  },  
  meo\_navigation\_constellation: {  
    id: "meo\_navigation\_constellation",  
    name: "1,800 kg Navigation Constellation Satellite (50V Bus, 20,200 km Van Allen Outer Belt)",  
    orbitRegime: "MEO 20,200 km (High-Radiation Belt)",  
    sunlightCondition: "eclipse",  
    plasmaElectronTempKev: 8.0,  
    plasmaElectronDensityCm3: 2.5,  
    plasmaIonTempKev: 10.0,  
    plasmaIonDensityCm3: 2.5,  
    killerElectronFluxMev: 9.5e4, // Severe trapped electron belt  
    chassisShieldThicknessMm: 2.5, // Heavy radiation shielding  
    busVoltageV: 50.0,  
    hasActiveChargeMitigation: true,  
    components: \[  
      { id: "MAT-01", name: "GaAs Solar Array Coverglass (Conductive Coated)", type: "solar\_coverglass", bulkResistivityOhmM: 5.0e11, relPermittivity: 3.8, thicknessMm: 0.15, surfaceResistivityOhmSq: 3.0e6, capacitancePfCm2: 22.4, isolatedMetalAreaCm2: 0.02, grounded: true },  
      { id: "MAT-02", name: "Germanium-Coated Black Kapton MLI Blankets", type: "thermal\_blanket", bulkResistivityOhmM: 5.0e8, relPermittivity: 3.4, thicknessMm: 0.05, surfaceResistivityOhmSq: 4.0e5, capacitancePfCm2: 60.2, isolatedMetalAreaCm2: 0.05, grounded: true },  
      { id: "MAT-03", name: "Atomic Clock Frequency Synthesizer Multi-layer Board", type: "internal\_pcb", bulkResistivityOhmM: 2.0e13, relPermittivity: 4.2, thicknessMm: 2.00, surfaceResistivityOhmSq: 8.0e11, capacitancePfCm2: 1.9, isolatedMetalAreaCm2: 0.01, grounded: true },  
      { id: "MAT-04", name: "High-Power L-Band Coaxial Cable PTFE Dielectric", type: "cable\_insulation", bulkResistivityOhmM: 5.0e15, relPermittivity: 2.1, thicknessMm: 1.20, surfaceResistivityOhmSq: 5.0e14, capacitancePfCm2: 1.5, isolatedMetalAreaCm2: 0.00, grounded: true },  
      { id: "MAT-05", name: "Thermal Radiator Second Surface Quartz Mirrors", type: "radiator\_mirror", bulkResistivityOhmM: 1.5e12, relPermittivity: 3.8, thicknessMm: 0.15, surfaceResistivityOhmSq: 1.5e7, capacitancePfCm2: 22.4, isolatedMetalAreaCm2: 0.06, grounded: true }  
    \]  
  }  
};

/\*\*  
 \* Calculate thermal velocity and ambient plasma collection current densities (A/m2)  
 \*/  
export function calcAmbientPlasmaFlux(tempKev, densityCm3, isElectron \= true) {  
  const m \= isElectron ? CHARGESPACE\_CONSTANTS.ELECTRON\_MASS\_KG : CHARGESPACE\_CONSTANTS.PROTON\_MASS\_KG;  
  const q \= CHARGESPACE\_CONSTANTS.ELEMENTARY\_CHARGE\_C;  
  const tJoules \= tempKev \* 1000.0 \* q;  
  const nM3 \= densityCm3 \* 1.0e6;  
  // v\_th \= sqrt(8 \* k\_B \* T / (pi \* m))  
  const vTh \= Math.sqrt((8.0 \* tJoules) / (Math.PI \* m));  
  // Random thermal flux: J\_0 \= q \* n \* v\_th / 4  
  const j0 \= (q \* nM3 \* vTh) / 4.0;  
  return { vTh, j0 };  
}

/\*\*  
 \* Solve self-consistent surface floating potential V\_surf (Volts)  
 \* Current balance: J\_e \* exp(V/T\_e) \- J\_i \- J\_ph \- J\_se \= 0  
 \*/  
export function solveSurfacePotential(preset, comp) {  
  // Internal shielded components inside metallic Faraday cage have no direct plasma exposure  
  if (comp.type \=== "internal\_pcb" \|\| comp.type \=== "cable\_insulation" \|\| comp.type \=== "structural\_bracket") {  
    const vChassis \= preset.sunlightCondition \=== "sunlit" ? 1.5 : (preset.hasActiveChargeMitigation ? \-85.0 : \-420.0);  
    return {  
      vSurf: Number(vChassis.toFixed(1)),  
      vChassis: Number(vChassis.toFixed(1)),  
      deltaV: 0.0,  
      jElectronUaM2: 0.0,  
      jIonUaM2: 0.0,  
      jPhotoUaM2: 0.0  
    };  
  }

  const q \= CHARGESPACE\_CONSTANTS.ELEMENTARY\_CHARGE\_C;  
  const eFlux \= calcAmbientPlasmaFlux(preset.plasmaElectronTempKev, preset.plasmaElectronDensityCm3, true);  
  const iFlux \= calcAmbientPlasmaFlux(preset.plasmaIonTempKev, preset.plasmaIonDensityCm3, false);  
  const jPh0 \= preset.sunlightCondition \=== "sunlit" ? CHARGESPACE\_CONSTANTS.PHOTOELECTRON\_FLUX\_AM0\_A\_PER\_M2 : 0.0;  
    
  // Secondary electron yield delta\_se \~ 0.25  
  const deltaSe \= 0.25;  
  const jNetElectron \= eFlux.j0 \* (1.0 \- deltaSe);  
  const jPositiveSources \= iFlux.j0 \+ jPh0;

  // External surface equilibrium potential  
  let vSurfUncoated \= 0.0;  
  const tEv \= preset.plasmaElectronTempKev \* 1000.0;

  if (jNetElectron \> jPositiveSources) {  
    const ratio \= Math.max(1e-4, jPositiveSources / jNetElectron);  
    vSurfUncoated \= tEv \* Math.log(ratio);  
  } else {  
    vSurfUncoated \= 3.5;  
  }

  const vChassis \= preset.sunlightCondition \=== "sunlit" ? 1.5 : (preset.hasActiveChargeMitigation ? \-85.0 : \-420.0);  
    
  // Conductive coating (ITO, Carbon Kapton, Germanium) bleeds surface charge to chassis  
  const rSq \= comp.surfaceResistivityOhmSq;  
  let vSurf \= vSurfUncoated;  
  let deltaV \= Math.abs(vSurfUncoated \- vChassis);

  if (comp.grounded && rSq \<= CHARGESPACE\_CONSTANTS.MAX\_SURFACE\_RESISTIVITY\_OHM\_SQ) {  
    // Current bleeding across surface: Delta V \= J\_net \* R\_sq \* L\_eff  
    // For dissipative surfaces, Delta V is clamped to a few tens of volts  
    const bleedFactor \= Math.min(1.0, rSq / 1.0e9);  
    deltaV \= Math.min(125.0, 25.0 \+ 80.0 \* bleedFactor);  
    vSurf \= vChassis \- deltaV;  
  }

  return {  
    vSurf: Number(vSurf.toFixed(1)),  
    vChassis: Number(vChassis.toFixed(1)),  
    deltaV: Number(deltaV.toFixed(1)),  
    jElectronUaM2: Number((eFlux.j0 \* 1e6).toFixed(3)),  
    jIonUaM2: Number((iFlux.j0 \* 1e6).toFixed(3)),  
    jPhotoUaM2: Number((jPh0 \* 1e6).toFixed(3))  
  };  
}

/\*\*  
 \* Solve internal deep dielectric charging from penetrating relativistic electrons (E \> 1 MeV)  
 \*/  
export function solveInternalCharging(preset, comp) {  
  const tShieldMm \= Number(preset.chassisShieldThicknessMm \|\| 1.5);  
  // Relativistic electron transmission through Aluminum shielding:  
  // Flux decays exponentially with shield thickness: J\_int \= J\_0 \* exp(-t / lambda)  
  const lambdaAlMm \= 0.85; // Characteristic attenuation length for \~1-2 MeV electrons  
  const transmittedFraction \= Math.exp(-tShieldMm / lambdaAlMm);  
    
  // Penetrating flux in pA/cm2 (1 e- / (cm2\*s) \= 1.602e-7 pA/cm2)  
  const incidentFluxPicoAmps \= (preset.killerElectronFluxMev \* 4.0 \* Math.PI) \* 1.602e-7;  
  const jIntPicoAmps \= incidentFluxPicoAmps \* transmittedFraction;  
  const jIntAmpsPerM2 \= jIntPicoAmps \* 1e-12 \* 1e4; // convert pA/cm2 to A/m2

  // Steady-state electric field buildup: E\_int \= J\_int \* rho\_bulk (V/m)  
  // Max field is bounded by radiation-induced conductivity (RIC)  
  const rhoBulk \= Number(comp.bulkResistivityOhmM);  
  const eIntRaw \= jIntAmpsPerM2 \* rhoBulk;  
  // Account for radiation-induced conductivity lowering effective rho at high dose  
  const ricFactor \= 1.0 / (1.0 \+ Math.pow(eIntRaw / 5.0e6, 0.45));  
  const eIntVPerM \= eIntRaw \* ricFactor;

  // Stored Electrostatic Energy density: w \= 0.5 \* epsilon\_0 \* epsilon\_r \* E^2 (J/m3)  
  const epsR \= Number(comp.relPermittivity);  
  const eps \= CHARGESPACE\_CONSTANTS.EPSILON\_0\_F\_PER\_M \* epsR;  
  const energyDensityJM3 \= 0.5 \* eps \* Math.pow(eIntVPerM, 2);

  // Stored ESD arc energy on component surface: W\_esd \= 0.5 \* C \* (Delta V)^2  
  const cFaradPerM2 \= (Number(comp.capacitancePfCm2) \* 1e-12) \* 1e4;  
  const surfSol \= solveSurfacePotential(preset, comp);  
  const wEsdJoules \= 0.5 \* cFaradPerM2 \* Math.pow(surfSol.deltaV, 2);

  const breakdownMarginFactor \= CHARGESPACE\_CONSTANTS.DIELECTRIC\_BREAKDOWN\_FIELD\_V\_PER\_M / Math.max(1.0, eIntVPerM);  
  const breakdownMarginDb \= 20.0 \* Math.log10(breakdownMarginFactor);

  const isFieldSafe \= eIntVPerM \<= CHARGESPACE\_CONSTANTS.MAX\_DESIGN\_ELECTRIC\_FIELD\_V\_PER\_M;  
  const isFluxSafe \= jIntPicoAmps \<= CHARGESPACE\_CONSTANTS.MAX\_INTERNAL\_CURRENT\_DENSITY\_PA\_CM2;  
  const isDeltaVSafe \= surfSol.deltaV \<= CHARGESPACE\_CONSTANTS.MAX\_ALLOWABLE\_DIFF\_POTENTIAL\_V;

  return {  
    componentId: comp.id,  
    componentName: comp.name,  
    type: comp.type,  
    shieldThicknessMm: tShieldMm,  
    transmittedFraction: Number(transmittedFraction.toFixed(4)),  
    jIntPicoAmpsCm2: Number(jIntPicoAmps.toFixed(4)),  
    eIntVPerM: Number(eIntVPerM.toFixed(1)),  
    energyDensityJM3: Number(energyDensityJM3.toFixed(3)),  
    wEsdJoules: Number(wEsdJoules.toExponential(3)),  
    breakdownMarginFactor: Number(breakdownMarginFactor.toFixed(2)),  
    breakdownMarginDb: Number(breakdownMarginDb.toFixed(2)),  
    surfacePotential: surfSol,  
    isFieldSafe,  
    isFluxSafe,  
    isDeltaVSafe,  
    isOverallCompliant: isFieldSafe && isFluxSafe && isDeltaVSafe && comp.isolatedMetalAreaCm2 \<= CHARGESPACE\_CONSTANTS.MAX\_ISOLATED\_METAL\_AREA\_CM2  
  };  
}

/\*\*  
 \* Execute full spacecraft charging, plasma interaction, and dielectric ESD risk assessment  
 \*/  
export function analyzeSpacecraftCharging(preset) {  
  const compResults \= preset.components.map((c) \=\> solveInternalCharging(preset, c));  
    
  const maxDeltaV \= Math.max(...compResults.map((c) \=\> c.surfacePotential.deltaV));  
  const maxEInt \= Math.max(...compResults.map((c) \=\> c.eIntVPerM));  
  const maxJInt \= Math.max(...compResults.map((c) \=\> c.jIntPicoAmpsCm2));  
  const minBreakdownMarginDb \= Math.min(...compResults.map((c) \=\> c.breakdownMarginDb));  
  const maxIsolatedArea \= Math.max(...preset.components.map((c) \=\> c.isolatedMetalAreaCm2));  
  const maxChassisPotential \= Math.abs(compResults\[0\].surfacePotential.vChassis);

  // Inverted Potential Gradient on Solar Array:  
  // V\_cell \- V\_coverglass. In eclipse/substorm, if V\_cell (chassis grounded) is positive relative to coverglass, arc risk spikes.  
  const saComp \= compResults.find((c) \=\> c.type \=== "solar\_coverglass") \|\| compResults\[0\];  
  const busV \= Number(preset.busVoltageV \|\| 28.0);  
  const invertedGradientV \= Math.max(0.0, busV \- saComp.surfacePotential.deltaV);

  const compliantCount \= compResults.filter((c) \=\> c.isOverallCompliant).length;  
  const isSystemCompliant \= compliantCount \=== compResults.length &&  
                            maxDeltaV \<= CHARGESPACE\_CONSTANTS.MAX\_ALLOWABLE\_DIFF\_POTENTIAL\_V &&  
                            maxEInt \<= CHARGESPACE\_CONSTANTS.MAX\_DESIGN\_ELECTRIC\_FIELD\_V\_PER\_M &&  
                            maxChassisPotential \<= CHARGESPACE\_CONSTANTS.MAX\_ALLOWABLE\_CHASSIS\_POTENTIAL\_V;

  return {  
    preset,  
    maxDeltaV: Number(maxDeltaV.toFixed(1)),  
    maxEIntVPerM: Number(maxEInt.toFixed(1)),  
    maxJIntPicoAmpsCm2: Number(maxJInt.toFixed(4)),  
    minBreakdownMarginDb: Number(minBreakdownMarginDb.toFixed(2)),  
    maxIsolatedAreaCm2: Number(maxIsolatedArea.toFixed(3)),  
    maxChassisPotentialV: Number(maxChassisPotential.toFixed(1)),  
    invertedGradientV: Number(invertedGradientV.toFixed(1)),  
    compliantCount,  
    totalComponents: compResults.length,  
    isSystemCompliant,  
    components: compResults  
  };  
}  
