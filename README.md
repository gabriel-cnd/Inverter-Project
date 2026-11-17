# Single-Phase H-Bridge Inverter

Design, simulation, PCB development and experimental validation of a **1 kW single-phase H-bridge inverter** developed as part of the **Power Electronics II** course.

> **Project status (November 2026):** PLECS simulation models are available for open-loop operation, dead-time effects and compensation, closed-loop voltage control with P and PR regulators, and HIL-oriented electrothermal analysis. The first milestone report and supporting design documents are archived in the repository. The presence of a model does not by itself demonstrate successful real-time or experimental validation. Hardware design and experimental validation remain future project phases.

## Project Overview

The goal is to design, build and validate a DC/AC converter based on a single-phase H-bridge supplied by a DC voltage source. The reference configuration uses an **inductive output filter (L)** and a **resistive load (R)**.

A **grid-connected (grid-tied) configuration** with an AC grid and coupling inductance has been identified as a possible project extension. It is **not** a substitute for validating the mandatory reference configuration; grid connection would require additional synchronization, control and protection work.

The complete development cycle includes:

- PLECS converter modelling and control simulation;
- power semiconductors, output filter, gate-driver and snubber dimensioning;
- voltage/current measurement and protection circuits;
- four-layer PCB design in KiCad;
- Hardware-in-the-Loop (HIL) validation using a PLECS RT-BOX;
- embedded control on a Texas Instruments F2837x platform;
- assembly, measurements and experimental validation.

## Main Specifications

| Parameter                       | Requirement                                 |
| ------------------------------- | ------------------------------------------- |
| Converter topology              | Single-phase H-bridge                       |
| DC input voltage                | 400 V                                       |
| AC output voltage               | 230 V RMS                                   |
| Nominal output power            | 1 kW                                        |
| Switching frequency             | 40 kHz                                      |
| Reference load                  | Resistive (R)                               |
| Output filter                   | Inductive (L)                               |
| Maximum output-current THD      | 2%                                          |
| Maximum inductor current ripple | 30% of nominal RMS current                  |
| Control platform                | Texas Instruments F2837x, 180-pin connector |
| PCB                             | 4 layers                                    |
| Target budget                   | < 100 CHF                                   |

For the full requirements, protections and safety constraints, see [cdc.md](cdc.md).


## PLECS Simulation Models

The models are organized in `simulations/plecs/` to document the development of the control strategy.

| Model prefix                                 | Purpose                                                                 | Current state                          |
| -------------------------------------------- | ----------------------------------------------------------------------- | -------------------------------------- |
| `01_Inverter_OpenLoop`                       | Initial H-bridge inverter in open loop                                  | Model available                        |
| `02_Inverter_OpenLoop_DeadTime`              | Introduction of dead time in switching signals                          | Model available                        |
| `03_Inverter_OpenLoop_DeadTime_Compensation` | Compensation of the dead-time-induced output error                      | Model available                        |
| `04_Inverter_ClosedLoop_Voltage_P_...`       | Closed-loop voltage control with a proportional (P) regulator           | Model available; performance to verify |
| `05_Inverter_ClosedLoop_Voltage_PR_...`      | Closed-loop voltage control with a proportional-resonant (PR) regulator | Model available; performance to verify |

*The last two names are abbreviated here because only their prefixes were confirmed. The actual `.plecs` files in the folder are authoritative.*

### HIL / RT-BOX preparation

Models in `simulations/HIL/`:

| File                                                   | Purpose                                   |
| ------------------------------------------------------ | ----------------------------------------- |
| `HIL_01_Inverter_OpenLoop.plecs`                       | HIL-oriented open-loop model              |
| `HIL_02_Inverter_OpenLoop_DeadTime.plecs`              | HIL-oriented dead-time model              |
| `HIL_03_Inverter_OpenLoop_DeadTime_Compensation.plecs` | HIL-oriented dead-time compensation model |
| `HIL_04_Inverter_OpenLoop_MOSFET_Thermal.plecs`        | HIL-oriented electrical and MOSFET thermal model |
| `Template_TI_RT_Box.plecs`                             | Reference RT-BOX template                 |

These files document **preparation for HIL**. Offline simulation and successful execution on the physical RT-BOX must be reported separately once demonstrated.

## Development Workflow

### 1. Simulation and control

Model the power stage, inductive filter and load in PLECS. Compare open-loop switching, dead-time effects, compensation and closed-loop regulation. Evaluate output voltage, current waveform, ripple and THD against the specifications.

### 2. Component dimensioning

Select the power semiconductors and calculate conduction/switching losses. Size the heatsink, gate drivers, snubbers, measurement circuits, output inductance and protection circuits. Add thermal models to PLECS when evaluating the selected devices.

### 3. PCB design

Develop the schematic and four-layer PCB in KiCad, considering **800 V insulation constraints**, electromagnetic compatibility, thermal management, measurement, gate driving and protection.

### 4. HIL validation

Verify the adapted controller and plant models with the RT-BOX, first offline using the template and then in real time on the hardware, as required for the first milestone.

### 5. Assembly and experimental validation

After safety checks, assemble the hardware and perform progressive, current-limited low-voltage tests before any nominal-voltage testing. Compare experimental results with simulation and design calculations.

## First Milestone

The first submission and the corresponding report are archived under `docs/rendus/01/`. They cover:

- application choice, objectives, specifications and converter operating principle;
- open-loop PLECS simulation and relevant results;
- selection and justification of the Wolfspeed `C3M0060065D` SiC MOSFET;
- loss estimation, heatsink sizing and a PLECS thermal model;
- preparation of the offline and HIL-oriented RT-BOX models.

The report distinguishes offline results from real-time measurements; successful execution on the physical RT-BOX still requires separate evidence.

## Repository Structure

```text
Inverter-Project/
├── README.md
├── cdc.md
├── diary.md
├── Mini_Project_conception_ELPU2.pdf
├── docs/
│   ├── report/                # LaTeX report workspace
│   └── rendus/                # Milestone instructions and submitted reports
├── simulations/
│   ├── plecs/                 # Offline PLECS models (01 to 05)
│   ├── HIL/                   # RT-BOX-oriented and thermal models, plus template
│   ├── matlab/
│   └── python/
├── datasheets/                # Selected MOSFET datasheet and PLECS loss model
├── hardware/
│   ├── kicad/
│   ├── bom/
│   ├── gerber/
│   └── manufacturing/
├── firmware/
├── measurements/
│   ├── raw/
│   └── processed/
├── scripts/
└── .gitignore
```

Some directories are reserved for upcoming project phases and may currently be empty.

## Software and Tools

- **PLECS:** power-stage and control simulations.
- **PLECS RT-BOX:** planned real-time HIL validation.
- **KiCad:** circuit schematic and PCB layout.
- **Texas Instruments F2837x:** target digital control platform.
- **LaTeX:** technical report.
- **Git / GitHub:** version control and collaboration.

## Documentation

- [Requirements and safety constraints](cdc.md)
- [Project decisions and development log](diary.md)
- [Official project description](Mini_Project_conception_ELPU2.pdf)
- [First milestone documents](docs/rendus/01/)
- [Driver and snubber design guide](docs/rendus/02/Mini_Projet_conception_ELPU2_driversnubber.pdf)
- [Wolfspeed C3M0060065D datasheet](datasheets/Wolfspeed_C3M0060065D_datasheet.pdf)

**Safety:** the project involves a nominal 400 V DC bus. Simulation files alone do not establish hardware safety or compliance. Experimental testing requires the project's specified electrical protections and supervised commissioning procedures.
