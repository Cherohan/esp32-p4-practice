# esp32‑p4‑practice

## Log
2026/8/16     Scheme done

2026/10/15    Schematic done

2026/10/30    PCB(V1) layout done

2026/10/31    ADS simulation done

2026/11/1     github done

## Project Intro
This repository contains hardware design files, ADS simulation projects and related documentation for ESP32‑P4 hardware platform.
This board is designed as an **industrial control board**, integrating abundant on‑board isolated industrial interfaces and high‑speed multimedia peripherals.

## Hardware Features
- **MCU**: ESP32‑P4 QFN‑104, 40 MHz external crystal oscillator
- **Storage**: W25Q512JVFQ 512 Mbit SPI Flash, 4‑bit SDIO MicroSD with hardware power‑gating
- **Ethernet**: 100 M Ethernet (IP101GRI PHY + isolated magnetics)
- **Isolated Industrial Interfaces**:
  - 3 × Isolated CAN 2.0
  - 2 × Isolated RS485
  - 1 × Isolated RS232
- **High‑speed Interfaces**: 2‑lane MIPI‑CSI, 2‑lane MIPI‑DSI, USB2.0 Type‑C
- **Audio**: ES8311 codec + NS4158 power amplifier, MIC input & speaker output
- **Analog Acquisition**: **12‑ch external ADC** with ESD/TVS protection and signal conditioning
- **On‑board Peripherals**: SHT30 temperature & humidity sensor, buzzer, 6×RGB LED, dedicated I2C‑OLED port
- **Expansion Headers**: I2C ×2, I3C, UART, multi‑purpose GPIO, FPC connectors for camera & display
- **Power Design**: Multi‑domain DCDC/LDO, independent isolated power for industrial transceivers, power‑gating for SD / OLED, RTC battery backup

## Hardware Block Diagram
![Hardware Block Diagram](./assets/Hardware-Block-Diagram.png)

## Power Tree
![Power Tree](./assets/power-tree.png)

The pcb layout preview is as follows:

![3d view top layer](./assets/3d_view_top.png)

![3d view bottom layer](./assets/3d_view_bottom.png)

![top layer](./assets/top_layer.png)

![inner1 layer](./assets/inner1_layer.png)

![inner2 layer](./assets/inner2_layer.png)

![inner3 layer](./assets/inner3_layer.png)

![inner4 layer](./assets/inner4_layer.png)

![bottom layer](./assets/bottom_layer.png)

## Signal & Power Integrity Simulation
### V1
After the PCB layout was completed, SI/PI simulations were conducted for all high-speed interfaces of the board using ADS.
The project contains complete ADS project files, simulation raw data, eye‑diagram reports and TDR/S‑parameter plots.

### Results
  1.The MIPI CSI/DSI performed well and passed TDR and S-parameter simulations.
  2.The network impedance of the PHY TDR section is relatively low, and reverse pad operation is required. There are several sudden impedance changes, and reflow vias need to be added, as well as new packet ground vias.
  3.The remaining high-speed signals need to add return vias and ground cover vias.
  4.SDIO has multiple impedance discontinuities and reflections, which require reverse pads, reflow vias, etc.

#### MIPI‑CSI Simulation
Simulate 2‑lane MIPI‑CSI clock + data lanes, swept series‑termination resistance (10 R /15 R /22 R).
Includes eye‑diagram report, TDR and S‑parameter curves for CLK, D0, D1 differential pairs.

10R
TDR

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-10R-TDR.jpg)

CLK

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-clk-10R-s.jpg)

D0

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-d0-10R-s.jpg)

D1

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-d1-10R-s.jpg)

15R
TDR

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-15R-TDR.jpg)

CLK

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-clk-15R-s.jpg)

D0

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-d0-15R-s.jpg)

D1

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-d1-15R-s.jpg)

22R
TDR

TDR

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-22R-TDR.jpg)

CLK

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-clk-22R-s.jpg)

D0

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-d0-22R-s.jpg)

D1

![MIPI‑CSI Simulation Results](./assets/mipi-csi/MIPI-CSI-d1-22R-s.jpg)

eyediff_eye
eyediff_porbel_0rj_0CDC

![MIPI‑CSI Simulation Results](./assets/mipi-csi/eyediff_porbel_0rj_0CDC.png)

eyediff_porbel_0_005rj

![MIPI‑CSI Simulation Results](./assets/mipi-csi/eyediff_porbel_0_005rj.png)

eyediff_porbel_data-dcd-0_005_clock-dcd-0_001

![MIPI‑CSI Simulation Results](./assets/mipi-csi/eyediff_porbel_data-dcd-0_005_clock-dcd-0_001.png)

eyediff_porbel_rj_0_005_data-dcd-0_005_clock-dcd-0_001

![MIPI‑CSI Simulation Results](./assets/mipi-csi/eyediff_porbel_rj_0_005_data-dcd-0_005_clock-dcd-0_001.png)

#### MIPI‑DSI Simulation
2‑lane MIPI‑DSI differential‑pair simulation, same termination‑resistor sweep strategy as CSI.
Evaluate eye opening, reflection and insertion loss for display high‑speed lanes.

10R
TDR

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-10R-TDR.jpg)

CLK

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-CLK-10R-S.jpg)

D0

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-D0-10R-S.jpg)

D1

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-D1-10R-S.jpg)

15R
TDR

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-15R-TDR.jpg)

CLK

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-CLK-15R-S.jpg)

D0

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-D0-15R-S.jpg)

D1

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-D1-15R-S.jpg)

22R
TDR

TDR

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-22R-TDR.jpg)

CLK

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-CLK-22R-S.jpg)

D0

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-D0-22R-S.jpg)

D1

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/MIPI-DSI-D1-22R-S.jpg)

eyediff_eye
eyediff_porbel_0rj_0CDC

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/eyediff_porbel_0rj_0CDC.png)

eyediff_porbel_0_005rj

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/eyediff_porbel_0_005rj.png)

eyediff_porbel_data-dcd-0_005_clock-dcd-0_001

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/eyediff_porbel_data-dcd-0_005_clock-dcd-0_001.png)

eyediff_porbel_rj_0_005_data-dcd-0_005_clock-dcd-0_001

![MIPI‑CSI Simulation Results](./assets/mipi-dsi/eyediff_porbel_rj_0_005_data-dcd-0_005_clock-dcd-0_001.png)

#### Ethernet PHY (phy‑p4 & phy‑rj)
Simulate 100 M Ethernet path: 50 MHz reference clock, TX/RX data lines, TX_EN, RJ45 + magnetics channel.
TDR & S‑parameter analysis to guarantee 100 Ω differential impedance of Ethernet pairs.

phy-p4 single Z50
TDR

![Ethernet PHY Simulation Results](./assets/phy-p4/PHY-P4-TDR.jpg)

RXD0

![Ethernet PHY Simulation Results](./assets/phy-p4/PHY-P4-RXD0-S.jpg)

RXD1

![Ethernet PHY Simulation Results](./assets/phy-p4/PHY-P4-RXD1-S.jpg)

RXDV

![Ethernet PHY Simulation Results](./assets/phy-p4/PHY-P4-RXDV-S.jpg)

TXD0

![Ethernet PHY Simulation Results](./assets/phy-p4/PHY-P4-TXD0-S.jpg)

TXD1

![Ethernet PHY Simulation Results](./assets/phy-p4/PHY-P4-TXD1-S.jpg)

TXEN

![Ethernet PHY Simulation Results](./assets/phy-p4/PHY-P4-TXEN-S.jpg)

PHY_50MCLK(P4-RXCLK)

![Ethernet PHY Simulation Results](./assets/phy-p4/PHY-P4-50MCLK-S-1.jpg)

PHY_50MCLK(P4-TXCLK)

![Ethernet PHY Simulation Results](./assets/phy-p4/PHY-P4-50MCLK-S-2.jpg)

phy-rj diff Z100
TDR

![Ethernet PHY Simulation Results](./assets/phy-rj/PHY-RJ-TDR.jpg)

RD

![Ethernet PHY Simulation Results](./assets/phy-rj/PHY-RJ-RD-S.jpg)

TD

![Ethernet PHY Simulation Results](./assets/phy-rj/PHY-RJ-TD-S.jpg)


#### SDIO Simulation (sdio‑sdcard & sdio‑wifi)
4‑bit SDIO bus single‑ended simulation, sweep series resistance (0 R ~33 R).
TDR for impedance check, S‑parameter for frequency‑response of CLK, CMD, D0~D3 lines.

SDIO-WIFI
0R
TDR

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-0R-TDR.jpg)

CLK

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-CLK-0R-S.jpg)

CMD

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-CMD-0R-S.jpg)

D0

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D0-0R-S.jpg)

D1

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D1-0R-S.jpg)

D2

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D2-0R-S.jpg)

D3

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D3-0R-S.jpg)

10R
TDR

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-10R-TDR.jpg)

CLK

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-CLK-10R-S.jpg)

CMD

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-CMD-10R-S.jpg)

D0

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D0-10R-S.jpg)

D1

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D1-10R-S.jpg)

D2

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D2-10R-S.jpg)

D3

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D3-10R-S.jpg)

15R
TDR

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-15R-TDR.jpg)

CLK

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-CLK-15R-S.jpg)

CMD

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-CMD-15R-S.jpg)

D0

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D0-15R-S.jpg)

D1

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D1-15R-S.jpg)

D2

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D2-15R-S.jpg)

D3

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D3-15R-S.jpg)

22R
TDR

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-22R-TDR.jpg)

CLK

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-CLK-22R-S.jpg)

CMD

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-CMD-22R-S.jpg)

D0

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D0-22R-S.jpg)

D1

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D1-22R-S.jpg)

D2

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D2-22R-S.jpg)

D3

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D3-22R-S.jpg)

33R
TDR

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-33R-TDR.jpg)

CLK

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-CLK-33R-S.jpg)

CMD

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-CMD-33R-S.jpg)

D0

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D0-33R-S.jpg)

D1

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D1-33R-S.jpg)

D2

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D2-33R-S.jpg)

D3

![SDIO-WIFI Results](./assets/sdio-wifi/SDIO-WIFI-D3-33R-S.jpg)

SDIO-SDCARD
0R
TDR

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-0R-TDR.jpg)

CLK

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-CLK-0R-S.jpg)

CMD

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-CMD-0R-S.jpg)

D0

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D0-0R-S.jpg)

D1

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D1-0R-S.jpg)

D2

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D2-0R-S.jpg)

D3

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D3-0R-S.jpg)

10R
TDR

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-10R-TDR.jpg)

CLK

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-CLK-10R-S.jpg)

CMD

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-CMD-10R-S.jpg)

D0

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D0-10R-S.jpg)

D1

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D1-10R-S.jpg)

D2

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D2-10R-S.jpg)

D3

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D3-10R-S.jpg)

15R
TDR

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-15R-TDR.jpg)

CLK

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-CLK-15R-S.jpg)

CMD

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-CMD-15R-S.jpg)

D0

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D0-15R-S.jpg)

D1

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D1-15R-S.jpg)

D2

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D2-15R-S.jpg)

D3

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D3-15R-S.jpg)

22R
TDR

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-22R-TDR.jpg)

CLK

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-CLK-22R-S.jpg)

CMD

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-CMD-22R-S.jpg)

D0

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D0-22R-S.jpg)

D1

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D1-22R-S.jpg)

D2

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D2-22R-S.jpg)

D3

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D3-22R-S.jpg)

33R
TDR

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-33R-TDR.jpg)

CLK

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-CLK-33R-S.jpg)

CMD

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-CMD-33R-S.jpg)

D0

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D0-33R-S.jpg)

D1

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D1-33R-S.jpg)

D2

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D2-33R-S.jpg)

D3

![SDIO-SDCARD Results](./assets/sdio-sdcard/SDIO-WIFI-D3-33R-S.jpg)

### Simulation Target & Spec
- MIPI CSI/DSI: Differential impedance target **100 Ω**
- Ethernet: Differential impedance target **100 Ω**
- SDIO: Single‑ended impedance target **50 Ω**
- PI: Power‑distribution‑network impedance analysis for high‑speed power domains

## Power‑Supply System Analysis
The board adopts **multi‑partition power‑domain architecture**, separating core high‑performance power, IO‑domain, memory power and isolated industrial power. This mitigates crosstalk between high‑speed core logic, analog circuits and noisy industrial field‑bus.

### Main Power Domains
1. **`ESP_3V3`**: IO‑domain power for ESP32‑P4, peripherals, sensors and logic circuits.
2. **`ESP_VDD_HP`**: High‑performance‑core power rail generated by DCDC chip `TLV62569DBVR`. Supplies P4 high‑speed logic, MIPI PHY, Ethernet PHY. This rail is a key PI simulation object in ADS.
3. **`VDD_FLASH`**: Dedicated power supply for QSPI Flash.
4. **`VDDO_PSRAM`**: PSRAM‑memory power rail (PCB reserved; PSRAM needs external soldering).
5. **`VDDO_3` / `VDDO_4`**: Other internal core‑power domains of ESP32‑P4, populated with dense local decoupling capacitors.
6. **`P4_vBAT`**: RTC backup‑power domain for real‑time‑clock operation during main‑power loss.
7. **Isolated auxiliary power**: Independent isolated power generated by ADUM‑series isolator internal power converter for CAN / RS485 / RS232 transceivers. Isolated GND is completely separated from main‑system GND to suppress ground‑loop interference from industrial environments.

### Peripheral Hardware Power‑Gating
- `SD_EN`: P‑MOS(AO3401) power‑switch for MicroSD card; software‑controlled power‑cut to reduce static power consumption.
- `OLED_EN`: MOS power‑switch for OLED display module; supports power‑down OLED during sleep mode.

### Power Protection & Decoupling Strategy
- Each power rail implements multi‑stage input filtering; TVS devices provide over‑voltage protection on external power‑input terminals.
- Every core‑power pin of ESP32‑P4, Flash, PHY and codec is placed with nearby 100 nF high‑frequency decoupling capacitor plus bulk capacitance for low‑frequency energy storage.
- DCDC‑output LC filter network optimizes switching noise for `ESP_VDD_HP`.

### Power‑Budget Considerations
- DCDC TLV62569 provides sufficient current margin for P4 high‑speed operation together with Ethernet and multimedia peripherals.
- Isolated industrial interfaces draw extra current; pay attention to total power‑budget when all CAN / 485 / 232 interfaces work simultaneously.

## Firmware Development Tips
- Target: ESP‑IDF for ESP32‑P4
- Drivers: MIPI‑DSI/CSI, SDIO, Ethernet, Isolated CAN/485/232, ADC, Audio codec
- State‑machine design recommended for multi‑industrial‑bus task scheduling.

## License