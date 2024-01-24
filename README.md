# PERT BMS Project

This project is intended to replace the previous BMS that has poor documentation and support. The first phase of this project is to build a fully functional BMS. The BMS doesn't need to be fancy, the only requirement for phase 1 is solid running.

## Timeline

| Milestone          | Time     |
|--------------------|----------|
| BSU HW design done | Jan 2024 |
| BSU SW design done | Feb 2024 |
| BSU stable version | Mar 2024 |
| BMU HW design done | Mar 2024 |
| BMU SW design done | Apr 2024 |
| BMU stable version | May 2024 |
| Fully function BMS | Jun 2024 |

## BMS Structure

![BMS General Structure](./Documents/IMG/BMS%20Structure-General%20Structure.png)

The BMS is a distributed BMS that uses a dedicated CAN bus to share information. The core modules are 5 BSUs and 1 BMU that monitor and protect the whole accumulator.
Each BSU (Battery Sampling Unit) corresponds to one battery segment. While BMU (Battery Monitoring Unit) is monitoring the whole battery pack and coordinating the BSUs.

### BMU Structure

![BMU Structure](./Documents/IMG/BMS%20Structure-BMU%20Structure.png)

The BMU uses an STM32F446 MCU and a BQ76931-Q1 Battery Monitoring Chip to monitor the battery pack status. This design simplifies the design of the monitoring circuit. The core of this module is the software to estimate the SOC, SOH, DOD, etc...
The second core is the software to control cell balancing between battery packs. The third is the charging and discharge control software.

### BSU Structure

![BSU Structure](./Documents/IMG/BMS%20Structure-BSU%20Structure.png)

The BSU uses an STM32F446 MCU, two BQ79616-Q1 and two ADS7951-Q1 to sense cell property. BQ89616-Q1 measures the voltage and performs cell balancing to the battery segment.
ADS7951-Q1  sensing the temperature of the battery.
The first core of the BSU is to sample all properties and broadcast them. The second core is to control the cell balancing to quickly balance the cell voltage with the limit of 8 cells per chip.

## PCB Design

The PCBs have 4 layers of copper and use JLCPCB standard stackup. 

### BSU PCB

The BSU is 100x255 mm with 6 mounting holes. The detailed PCB design is shown in the [Description](./BSU/Documents/BSU-Description.pdf) and [Schematic](./BSU/Documents/BSU-Schematic.pdf).
