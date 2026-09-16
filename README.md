# Single-Phase H-Bridge Inverter

Design, simulation, PCB development and experimental validation of a **1 kW single-phase H-bridge inverter** developed as part of the Power Electronics II course.

The project covers the complete development cycle of a power electronic converter, from the initial modelling and component sizing to PCB design, Hardware-in-the-Loop validation, assembly and experimental testing.

## Project Overview

The objective of this project is to design and build a fully operational single-phase DC/AC inverter based on an H-bridge topology.

The converter is supplied from a DC voltage source and generates a controlled AC output through an inductive output filter.

The development process includes:

- Converter modelling and simulation
- Power stage dimensioning
- Gate-driver design
- Snubber design
- Voltage and current measurement circuits
- Output filter dimensioning
- PCB schematic and layout
- Hardware-in-the-Loop validation
- Embedded control
- PCB assembly
- Experimental measurements and validation

## Main Specifications

| Parameter                       |                       Value |
| ------------------------------- | --------------------------: |
| Converter topology              |       Single-phase H-bridge |
| Input voltage                   |                    400 V DC |
| Output voltage                  |                   230 V RMS |
| Nominal power                   |                        1 kW |
| Switching frequency             |                      40 kHz |
| Base load                       |                   Resistive |
| Output filter                   |                   Inductive |
| Maximum current THD             |                         2 % |
| Maximum inductor current ripple | 30 % of nominal RMS current |
| Control platform                |    Texas Instruments F2837x |
| PCB                             |                    4 layers |
| Target PCB budget               |                   < 100 CHF |

## Development Workflow

The project is divided into several development phases:

### 1. Simulation

The inverter, output filter and load are modelled and validated using **PLECS**.

### 2. Component Dimensioning

The main electrical components are dimensioned, including:

- Power semiconductors
- Gate drivers
- Snubber circuits
- Current and voltage measurement circuits
- Output inductance
- Protection circuits

### 3. PCB Design

The complete converter PCB is designed using **KiCad**.

The design includes considerations related to:

- High-voltage isolation
- Power and signal routing
- Electromagnetic compatibility
- Thermal management
- Measurement circuits
- Gate-drive circuits
- Protection systems

### 4. Hardware-in-the-Loop

The control strategy is validated in real time using a Hardware-in-the-Loop platform before operating the physical converter.

### 5. Assembly and Experimental Validation

The PCB is assembled and tested progressively, starting at reduced voltage before operation at nominal conditions.

Experimental measurements are then compared with the theoretical calculations and simulation results.

## Software & Tools

- **PLECS** — converter modelling and simulation
- **KiCad** — schematic capture and PCB design
- **Texas Instruments F2837x** — digital control platform
- **Hardware-in-the-Loop** — real-time control validation
- **LaTeX** — technical documentation and final report
- **Git / GitHub** — version control and collaboration

Additional tools may be added during the development of the project.

## Repository Structure

```text
Inverter-Project/
│
├── docs/
│   └── report/
│
├── simulations/
│   └── plecs/
│
├── hardware/
│   └── kicad/
│
├── firmware/
│
├── measurements/
│
├── datasheets/
│
├── README.md
└── .gitignore