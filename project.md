# H.A.R.S — Hygroscopic Aerodynamic Restoration System
---

## GitHub Repository

`https://github.com/basilsaeedbari/hars-filament-dryer`

---

## Team Members

| Full Name | Student ID | GitHub Username | Habib Email | Program | Year | Role |
|---|---|---|---|---|---|---|
| Basil Saeed Bari | bb09892 | basilsaeedbari | bb09892@st.habib.edu.pk | CE | 3 | Lead |

---

## Abstract
An Open-Source, Ultra-Low-Cost Closed-Loop Active Convection Desiccant Chamber for 3D Printing Filament Restoration

Polymer hydration is the primary point of failure in 3D printing in high-humidity environments. In Karachi, where ambient relative humidity regularly exceeds 70–90%, hygroscopic filaments such as PLA, PETG, and Nylon rapidly absorb atmospheric moisture. This absorbed water vaporises explosively inside the extruder nozzle at printing temperatures, causing stringing, bubbling, poor layer adhesion, and structurally compromised prints. The H.A.R.S (Hygroscopic Aerodynamic Restoration System) project addresses this problem by engineering an ultra-low-cost, open-source, closed-loop active desiccant chamber that actively strips moisture from saturated filament using four integrated physical mechanisms: forced convection via a 3D-printed Venturi nozzle (Bernoulli's Principle), bulk moisture removal via a copper cold coil (phase-change condensation), trace humidity adsorption via an indicating silica gel bed, and precise thermal regulation via a PID control loop running on an ESP32 microcontroller. The system is designed entirely around scrap, repurposed, and locally sourced Pakistani market components, targeting a total Bill of Materials cost under ₨5,500. A successful outcome is defined as dropping internal relative humidity below 15% within 30 minutes of activation while maintaining a stable chamber temperature of 45°C ± 2°C — well below the glass transition temperature of the polymers being dried. All hardware schematics, 3D-printable STL files, and firmware will be released as open-source for the wider Pakistani maker and engineering community. Future milestones will progressively downscale the electronics stack from an ESP32 development board to bare-metal AVR ICs and ultimately to a sub-₨200 analogue control circuit.

---

## Problem Statement

In Karachi's high-humidity climate, 3D printing filament degradation due to moisture absorption is a persistent, unsolved problem for hobbyists, hardware engineers, and university makerspaces. Hygroscopic polymers — PLA, PETG, Nylon, TPU — absorb water at the molecular level from ambient air within hours of exposure. Once hydrated, the filament cannot simply be "used carefully"; the moisture must be physically extracted before printing. The two categories of available solutions are both inadequate for the local context.

Commercial active filament dryers (Sunlu, eSun, PrintDry) are imported products subject to heavy Pakistani customs duties, placing them in the ₨8,000–15,000 price range — unviable for student budgets. Beyond cost, these devices rely on brute-force convection heating that risks thermally warping the lower layers of a spool if left unattended, and they provide no feedback control to prevent this.

DIY passive dry boxes — airtight containers with loose silica gel — are the community's default response. However, these are preventive tools, not restorative ones. Stagnant air inside the box maintains a near-equilibrium humidity with the saturated silica, and without forced convection, the Vapor Pressure Deficit driving moisture out of the filament approaches zero. A heavily hydrated spool of PETG requires many days in a passive dry box to reach printable moisture levels. There is a critical, unmet need for an accessible, reproducible, restorative drying system that applies the correct physics — forced convection, phase-change condensation, and active desiccation — to rapidly restore hydrated filament to printable condition, built entirely from components available in the Pakistani local market.

---

## Domain & IEEE Alignment

**Primary Domain:**
- [ ] Electrical Engineering
- [ ] Computer Science
- [x] Computer Engineering
- [ ] Mechatronics / Robotics
- [ ] Telecommunications
- [ ] Power Systems
- [ ] Signal Processing
- [ ] Other: _______________

**Sub-Field / Specialization:**  
`Embedded Systems & Mechatronics`

**Relevant IEEE Technical Society:**  
`IEEE Robotics and Automation Society`

**Applicable IEEE Standard(s), if any:**  
`None directly applicable`

---

## Objectives

1. To design and fabricate a closed-loop Venturi airflow system using custom 3D-printed nozzles that demonstrably increases air velocity across the filament spool surface by at least 50% compared to standard axial fan placement, as verified by anemometer measurement.
2. To implement a software PID control loop on an ESP32 microcontroller that maintains the drying chamber temperature at 45°C ± 2°C using a 104K NTC thermistor and a logic-level MOSFET-switched ceramic heating element, with a measured step-response overshoot of less than 5°C.
3. To integrate a multi-stage moisture extraction path — copper cold coil (bulk condensation) followed by an indicating silica gel bed (trace adsorption) — that reduces internal chamber relative humidity to below 15% within 30 minutes of system activation, as logged by an independent digital hygrometer.
4. To quantify the system's restorative capacity by measuring the mass of water extracted from a heavily pre-hydrated 1kg PETG spool over a 4-hour drying cycle using a precision gram scale, targeting a minimum of 2g of extracted moisture.
5. To deliver a complete Prototype 1 system with a total Bill of Materials cost under ₨5,500, using exclusively repurposed, scrap-market, and locally sourced Pakistani components, with all costs documented in a public expense ledger.
6. To produce a fully open-source hardware and firmware release — including KiCad schematics, 3D-printable STL files, calibrated ESP32 firmware, and a documented migration pathway — enabling transition to a bare-metal AVR microcontroller for a target sub-₨2,500 Phase 3 unit cost.

---

## Methodology

### The Engineering Integration: Why This is a Complex Multidisciplinary Project

H.A.R.S is not a firmware project with a box around it, nor is it a mechanical project with a microcontroller bolted on. It is an exercise in tight multidisciplinary integration where the mechanical and electronic subsystems are co-dependent. The Venturi nozzle geometry determines the Reynolds number and turbulence regime inside the chamber, which in turn sets the convective heat transfer coefficient that the PID algorithm must compensate for. The cold coil's thermal mass affects the rate at which the chamber temperature drops during the condensation cycle, directly influencing the PID's integral windup behaviour. Every mechanical design decision has a corresponding embedded systems consequence, and vice versa.

The project leverages the following engineering processes simultaneously:

**Mechanical Engineering processes:** Computational Fluid Dynamics (CFD) simulation of Venturi nozzle geometry; thermodynamic analysis of the dew-point condensation stage; heat transfer modelling of the ceramic heater-to-air interface; structural analysis of 3D-printed PLA/PETG parts under sustained thermal load; and fabrication tolerancing for airtight fitment of all bulkheads and seals.

**Computer Engineering processes:** Embedded C++ firmware development; ADC-based thermistor characterisation using the Steinhart-Hart equation; PID algorithm implementation and iterative gain tuning (Ziegler-Nichols method); logic-level power electronics design (MOSFET gate drive circuit); PWM frequency selection for heater and fan control; real-time safety interrupt design; and a documented hardware abstraction pathway from ESP32 to bare-metal AVR architecture.

### Design & Simulation Phase

The mechanical enclosure and Venturi nozzle will be designed in Fusion 360, targeting a parametric model that allows nozzle taper angle to be adjusted for CFD validation. Basic fluid dynamics simulations will be run in SimScale (OpenFOAM cloud solver) to compare air velocity profiles at the spool surface for different nozzle geometries, with the target of achieving at least 50% velocity increase over standard fan placement. Thermal simulations will model the heat distribution from the ceramic element to verify no localised hot spots exceed 60°C before the airflow path equilibrates.

The full electronics circuit — ESP32, buck converter, MOSFET gate drive, thermistor voltage divider, and heater load — will be modelled and simulated in Proteus Design Suite. The simulation will verify correct logic-level switching behaviour, gate resistor sizing to prevent oscillation, and the thermal protection relay logic before any physical components are soldered.

### Hardware / Software Implementation Phase

**Enclosure:** A large airtight plastic storage tub will be modified with custom 3D-printed bulkheads to mount the fan intakes, Venturi nozzle exit, cold coil inlet, and solar chimney exhaust port. All penetrations will be sealed with high-temperature RTV silicone to maintain airtightness during operation.

**Airflow loop:** Two repurposed 16k RPM server fans will be mounted in series to drive air through the cold coil, the silica gel tray, and into the Venturi nozzle. The silica gel bed will be housed in a removable mesh tray to allow easy regeneration. The copper cold coil will be formed by hand from standard plumbing tubing and chilled passively (ambient cold-side radiation) in the initial prototype, with provision for an active Peltier module in a later revision.

**Electronics:** The circuit will be assembled on perfboard for Prototype 1. The ESP32 reads the NTC thermistor via a 10kΩ voltage divider into an ADC pin, applies the Steinhart-Hart conversion in firmware, and runs the PID loop at 1Hz. The PID output drives a PWM signal to the IRLZ44N MOSFET gate (via a gate resistor), which controls the ceramic heater in the 12V rail. A 10kΩ pull-down on the gate guarantees heater-off during boot. The buck converter drops 12V to 5V for ESP32 logic power.

**Firmware:** Written in C++ using the Arduino-ESP32 framework. Key modules include: thermistor ADC sampling and Steinhart-Hart conversion, PID control loop with anti-windup, PWM fan speed control, safety watchdog (hardware cutoff at 60°C and on fan-stall detection via tachometer input), and serial telemetry output for real-time data logging during testing.

### Testing & Validation Phase

**Airflow:** Air velocity at the Venturi nozzle exit and at the spool surface will be measured using a digital anemometer, compared against baseline (direct fan placement) to quantify the Venturi gain.

**Thermal:** The PID step response will be logged via serial telemetry. A Python script will plot the step response curve to characterise rise time, overshoot, and steady-state error. PID gains will be iteratively tuned using the Ziegler-Nichols method until the overshoot criterion (<5°C) is met.

**Drying performance:** A 1kg spool of PETG will be deliberately hydrated by exposure to open air for 72 hours. It will be weighed on a precision gram scale (±0.1g resolution) before being placed in the chamber. The chamber's internal temperature and relative humidity will be logged every 60 seconds by an independent digital hygrometer (not the NTC) for the duration of the 4-hour test cycle. The spool will be reweighed at the end to calculate total extracted moisture mass. Print quality of the first 100g extruded after drying will be evaluated visually and by comparing dimensional accuracy of a calibration print against a baseline dry-spool print.

---

## Work Breakdown Structure (WBS)

| Milestone # | Milestone Name | Key Deliverables | Start Date | End Date | Status |
|---|---|---|---|---|---|
| M1 | Design & Simulation | Fusion 360 assembly model; CFD velocity comparison report; Proteus circuit simulation with verified MOSFET switching logic | 2026-05-15 | 2026-05-28 | Not Started |
| M2 | Component & Material Procurement | All components sourced and physically received; verified against BOM; photographs of each component | 2026-05-29 | 2026-06-05 | Not Started |
| M3 | Prototype 1 Build (ESP32) | Assembled and airtight enclosure; wired electronics on perfboard; baseline firmware uploaded and running; initial serial telemetry confirmed | 2026-06-06 | 2026-06-22 | Not Started |
| M4 | Testing, PID Tuning & Validation | Step-response graph with gains documented; 4-hour drying test log (CSV); spool mass-loss measurement; hygrometer humidity log; print quality comparison | 2026-06-23 | 2026-07-07 | Not Started |
| M5 | Open-Source Release & Documentation | KiCad schematics exported to PDF; all STLs published; firmware on GitHub with README; final technical report; Phase 2 AVR migration schematic draft | 2026-07-08 | 2026-07-18 | Not Started |

**Estimated Total Duration:** `9 weeks`

---

## Resource Management Matrix

| Resource | Lab / Location | Estimated Hours | Purpose in Project | Required From | Required Until |
|---|---|---|---|---|---|
| Oscilloscope (2-channel) | Electronics Lab | 8 hrs | Verifying PWM waveform to MOSFET gate; checking gate resistor damping; confirming thermistor ADC signal integrity | 2026-06-06 | 2026-06-22 |
| Soldering Station | Electronics Lab | 12 hrs | Perfboard assembly of full electronics circuit; wire harnessing and connector crimping | 2026-06-06 | 2026-06-22 |
| Prusa i3 MK3S+ | Makerspace | 20 hrs | Fabricating Venturi nozzle (PETG), spool tray (PETG), silica bed housing (PETG), and fan bulkhead adapters (PLA) | 2026-05-29 | 2026-06-10 |
| Digital Multimeter | Electronics Lab | 6 hrs | Buck converter output verification; MOSFET gate voltage measurement; voltage divider calibration | 2026-06-06 | 2026-06-22 |
| Precision Gram Scale (±0.1g) | Makerspace / Science Lab | 2 hrs | Pre- and post-drying spool mass measurement to quantify extracted moisture | 2026-06-23 | 2026-07-07 |

- [x] I have read Schedule A of the Terms & Conditions and will complete all required safety training before using listed Tier 2/3 equipment.

---

## Risk Assessment

| Risk | Likelihood (H/M/L) | Impact (H/M/L) | Mitigation Strategy |
|---|---|---|---|
| MOSFET or heater thermal runaway causing enclosure deformation or fire | L | H | 10kΩ pull-down on gate (hardware-level heater-off at boot); 60°C software cutoff; 72°C hardware thermal fuse in series with heater circuit; ceramic heater mounted on aluminium heatsink inside airflow path, not touching plastic. |
| Inability to source identical 16k RPM server fans | M | M | Venturi nozzle designed as a parametric Fusion 360 model; taper angle adjustable to compensate for different fan CFM ratings. Multiple fan sizes tested in simulation before fabrication. Shershah market surveyed for available fan models before M1 closes. |
| PID loop instability causing sustained temperature oscillation | M | M | Ziegler-Nichols tuning method applied systematically. Anti-windup implemented in firmware. If software PID is insufficient, a hardware RC low-pass filter will be added on the gate drive signal to damp rapid switching. |
| Airtight enclosure seal failure reducing drying efficiency | M | L | All bulkhead penetrations sealed with high-temperature RTV silicone. A simple "pressure test" (sealing all ports and applying gentle positive pressure with a bicycle pump, observing for leaks via soap solution) performed before the M4 validation tests. |
| Cold coil insufficient to drop air below dew point at ambient Karachi temperatures | M | H | Passive cold coil is the baseline design. Provision made in enclosure design for a 12V Peltier module (TEC1-12706, ~₨800 locally) as a drop-in upgrade if passive condensation proves insufficient in testing. |
| 3D-printed PETG parts deforming under sustained 45°C operating temperature | L | M | PETG glass transition is ~80°C; parts in the hot airflow path will be printed in PETG. Parts in the cold coil region may be PLA (Tg ~60°C). No printed parts will be in direct thermal contact with the heater element. |

---

## Success Metrics

| Metric | Target Value | Measurement Method |
|---|---|---|
| 1. Internal Chamber Humidity Reduction | Below 15% RH within 30 minutes of activation | Independent digital hygrometer (SHT31 or equivalent), logged at 60-second intervals via separate data logger |
| 2. Chamber Temperature Stability | 45°C ± 2°C steady-state | Serial telemetry from NTC thermistor; cross-validated with independent K-type thermocouple at M4 |
| 3. PID Step-Response Overshoot | Less than 5°C above setpoint | Step-response plot generated from serial log data in Python |
| 4. Moisture Extraction (Mass Loss) | Greater than 2.0g per 4-hour cycle from a pre-hydrated 1kg PETG spool | Precision gram scale (±0.1g), weigh before and after 4-hour cycle |
| 5. Total BOM Cost — Prototype 1 | Under ₨5,500 | Public expense ledger committed to `/docs/bom_v1.csv` |
| 6. Air Velocity Gain at Spool Surface | At least 50% increase over direct fan placement baseline | Digital anemometer measurement at spool surface with and without Venturi nozzle fitted |

---

## Project Updates

### Update Log

#### 2026-05-11 — Project Initialised

H.A.R.S repository created. `project.md` drafted and submitted to HOIISP. Design phase begins 2026-05-15. Fusion 360 and Proteus licenses confirmed. Local market survey for 16k RPM server fans to be conducted this week at Shershah.

---

## Data & Documentation Plan

- All KiCad schematic source files stored in `/hardware/schematics/`, with a PDF export for non-KiCad users.
- All 3D-printable STL files stored in `/hardware/stls/`, with the Fusion 360 master assembly in `/hardware/cad/`.
- ESP32 firmware (C++, Arduino framework) version-controlled in `/firmware/esp32/`.
- Future AVR and ATtiny firmware stored in `/firmware/avr/` and `/firmware/attiny/` respectively.
- All drying test CSV logs (timestamp, temperature, relative humidity) stored in `/data/test_logs/`.
- PID step-response plots stored as PNG in `/data/pid_tuning/`.
- Build-progress photographs stored in `/docs/photos/`, named by milestone and date.
- Full Bill of Materials stored as CSV in `/docs/bom_v1.csv`, with itemised receipts photographed and committed.
- SimScale CFD result exports (velocity contour images, data files) stored in `/sim/cfd/`.
- Proteus simulation project file stored in `/sim/proteus/`.

**Repo structure commitment:** I understand that the HOIISP project page links directly to this repository. The repo should be organised and have a readable top-level README.

- [x] Confirmed.

---

## Budget Estimate

| Item | Source | Estimated Cost (PKR) |
|---|---|---|
| ESP32 Development Board | Local Electronics Market (Saddar) | 1,200 |
| Used 16k RPM Server Fans (×2) | Shershah / Scrap Market | 800 |
| Logic-Level MOSFET (IRLZ44N or equiv.) | Local Electronics Market | 150 |
| 104K NTC Thermistor | Local Electronics Market | 100 |
| 10kΩ Resistors & Gate Resistor (assorted) | Local Electronics Market | 50 |
| PTC Ceramic Heater (12V) | Daraz / Local | 750 |
| 12V 5A Power Supply (used/repurposed) | Shershah / Used Market | 600 |
| Buck Converter Module (LM2596 or equiv.) | Local / Daraz | 200 |
| Indicating Silica Gel (500g) | Local Chemical Supplier | 500 |
| Copper Tubing for Cold Coil (~0.5m) | Plumbing Supply Shop | 300 |
| Large Airtight Plastic Storage Tub | Supermarket / Utility Store | 500 |
| PETG Filament for 3D-Printed Parts (~150g) | Makerspace / Daraz | 400 |
| High-Temp RTV Silicone Sealant | Hardware Store | 250 |
| Misc. (wire, connectors, perfboard, zip ties, terminal blocks) | Local | 300 |
| | **Total Estimated:** | **₨6,100** |

> Note: Target is under ₨5,500 after sourcing optimisation (e.g., repurposing existing wire stock, using university lab perfboard). The ₨6,100 figure is a conservative upper bound. All actual expenditure will be tracked in `/docs/bom_v1.csv`.

---

## References

[1] H. K. Versteeg and W. Malalasekera, *An Introduction to Computational Fluid Dynamics: The Finite Volume Method*, 2nd ed. Pearson Education, 2007.  
[2] K. Ogata, *Modern Control Engineering*, 5th ed. Prentice Hall, 2010.  
[3] J. G. Ziegler and N. B. Nichols, "Optimum settings for automatic controllers," *Trans. ASME*, vol. 64, pp. 759–768, 1942.  
[4] Espressif Systems, *ESP32 Technical Reference Manual*, v5.3, 2024. [Online]. Available: https://www.espressif.com/sites/default/files/documentation/esp32_technical_reference_manual_en.pdf  
[5] Infineon Technologies (formerly International Rectifier), *IRLZ44N HEXFET Power MOSFET*, Product Datasheet, Rev. B. [Online]. Available: https://www.infineon.com/dgdl/irlz44npbf.pdf  
[6] Y. A. Çengel and M. A. Boles, *Thermodynamics: An Engineering Approach*, 8th ed. McGraw-Hill, 2015.  
[7] Atmel Corporation, *ATmega328P Datasheet*, Rev. 8161D, 2013. [Online]. Available: https://ww1.microchip.com/downloads/en/DeviceDoc/Atmel-7810-Automotive-Microcontrollers-ATmega328P_Datasheet.pdf

---

## Declaration

- [x] I confirm that the information in this `project.md` is accurate and complete.
- [x] I have read and agree to the HOIISP Terms & Conditions in full.
- [x] I confirm that all listed team members are aware of this submission and have agreed to participate.
- [x] I confirm that at least one team member has committed to this repository using a `@st.habib.edu.pk` Git email address.
- [x] I understand that approval of this submission grants access only to the resources explicitly listed in the Resource Management Matrix.
- [x] I understand that I must push a `project.md` update at least once every two weeks to maintain Active project status and lab access.
- [x] I accept that all content parsed from this repository will be publicly visible on the HOIISP platform.
- [x] I confirm this repository is set to **Public** visibility on GitHub (HOIISP cannot read private repositories).

---

## For Office Use Only
> *Do not fill in this section.*

| Field | Value |
|---|---|
| HOIISP Submission ID | |
| GitHub Verification Status | |
| Assigned Project Slug | |
| Review Outcome | Approved / Rejected / Revisions Required |
| Review Notes | |
| Admin | |
| Date of Decision | |
| Resource Request Forwarded | |
| Lab Access Activated | |
