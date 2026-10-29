# ChargeSpaceForge Pro v1.0.0

> Spacecraft Surface & Internal Dielectric Charging, Plasma Interaction & ESD Arc Mitigation Studio

## Overview

ChargeSpaceForge Pro v1.0.0 is an enterprise aerospace engineering studio developed per [NASA-HDBK-4002A](https://standards.nasa.gov/), [ECSS-E-ST-20-06C](https://ecss.nl/), [NASA-STD-4010](https://standards.nasa.gov/), and [ISO 19923:2017](https://www.iso.org/). It provides rigorous differential surface potential budgeting (\$\\Delta V \\le 500	ext{ V}\$), internal deep dielectric charging (\$E\_{int} \\le 2.0	ext{ MV/m}\$ with 5x margin below \$10	ext{ MV/m}\$ breakdown), relativistic electron flux attenuation (\$J\_{int} \\le 0.10	ext{ pA/cm}^2\$), solar array inverted-gradient ESD prevention, and automated 10-point normative compliance auditing.

## Directory Structure

- `source-code/`: Pure ES6 physics engine, normative compliance auditor, Python CLI suite, unit test runner, and interactive HTML cockpit.  
- `build/`: Packaged standalone web studio application and distribution zip archive.  
- `documentation/`: Standards specifications, compliance matrices, executive summary, and user guides.  
- `screenshots/`: Visual studio previews and spacecraft charging architecture diagrams.

## Quick Start

\# Run unit test suite (10/10 PASS)

python3 source-code/test\_runner.py

\# Run Node.js normative audit

node source-code/chargespace-auditor.js

\# Run CLI audit on GEO Substorm

python3 source-code/chargespace\_cli.py audit \--preset geo\_severe\_substorm\_telecom

\# Export NASA XML Manifest

python3 source-code/chargespace\_cli.py export-xml \--preset meo\_navigation\_constellation

\# Open Interactive Web Cockpit in Browser

open build/chargespace\_forge\_pro\_studio.html