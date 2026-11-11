# Bill of Materials

| Field | Value |
|---|---|
| Project | A handheld clamshell outfit picker |
| BOM type | Engineering BOM, prototype build |
| Revision | A, November 11, 2026 |
| Build quantity | 1 unit |
| Prices | USD, checked on DigiKey and Amazon on Nov 11, 2026. Shipping and tax not included. |
| Stock | Every part to buy was in stock on Nov 11, 2026 |
---

## 1. Cost summary

| Group | Cash to buy | Cost per device |
|---|---|---|
| Lid: compute and display | $39.32 | $39.32 |
| Base: control PCB assembly | $49.75 to $64.75 | $32.57 to $35.57 |
| Power and cabling | $5.95 | $5.95 |
| Enclosure and mounting | $14.99 to $29.99 | $5.60 to $20.60 |
| Prototyping (not in the deck) | $9.95 | n/a |
| **Total to buy** | **$119.96 to $149.96** | |
| **Per-device cost of purchased parts** | | **$83.44 to $101.44** |
| Already owned (Zero 2 W kit, power bank, USB data cable, breadboard) | $0 | about $79.50 value |

**By store** (exact-price parts only): DigiKey $48.66 · Amazon $56.30

Ranges come from the two parts that aren't designed yet: the control PCB order ($10 to $25 for 5 boards) and the case ($5 to $20).

---

## 2. Assembly tree

```
0 Outfit Deck
├── 1.0 Lid: compute + display
│   ├── 1.1 Pi Zero 2 W kit (owned)
│   ├── 1.2 4.0" SPI screen
│   └── 1.3 microSD card
├── 2.0 Base: control PCB assembly
│   ├── 2.1 Control PCB (PCB1)
│   ├── 2.2 Pico 2 (U1)
│   ├── 2.3 Key switches ×11 (SW1–SW11)
│   ├── 2.4 Keycaps ×11
│   ├── 2.5 RGB LEDs ×11 (D1–D11)
│   ├── 2.6 Level shifter (U2)
│   ├── 2.7 Resistor (R1)
│   ├── 2.8 Bulk capacitor (C1)
│   ├── 2.9 Small caps ×12 (C2–C13)
│   ├── 2.10 Audio amp (U3)
│   ├── 2.11 Speaker (LS1)
│   ├── 2.12 Spare header (J1)
│   └── 2.13 Jumpers ×12 (JP1–JP12)
├── 3.0 Power + cabling
│   ├── 3.1 Power bank (owned)
│   ├── 3.2 On/off power cable
│   └── 3.3 USB data cable (owned)
└── 4.0 Enclosure + mounting
    ├── 4.1 Case / switch plate
    └── 4.2 M2.5 standoffs
```

---

## 3. Bill of materials

### 1.0 Lid: compute and display

| Item | Component | Model (link) · MFR part # | Qty / UOM | Price: pack → per device | Shipping time | Specs | Installation | Notes |
|---|---|---|---|---|---|---|---|---|
| 1.1 | Main computer | Raspberry Pi Zero 2 W Basic Kit (Zero 2 W, 40-pin header, heatsink, USB OTG adapter, mini-HDMI adapter) · Raspberry Pi SC0510 | 1 kit | Owned (about $71 kit) | Owned | Quad-core Arm Cortex-A53 at 1 GHz, 512 MB RAM<br>2.4 GHz Wi-Fi, Bluetooth 4.2<br>40-pin GPIO, micro-USB power in, micro-USB OTG data | Solder the kit's 40-pin header<br>Stick the heatsink on the main chip (clean with isopropyl alcohol first)<br>Mount in the lid on M2.5 standoffs | Runs the app, screen, closet storage and try-on requests. Mini-HDMI adapter is only for setup. |
| 1.2 | Screen | [DWEII 4.0" 480×320 SPI TFT, ST7796S](https://www.amazon.com/dp/B0CQXDXVPS) · Amazon B0CQXDXVPS | 1 EA | $17.99 → $17.99<br>Amazon | In stock<br>Prime: Fri Nov 13<br>Free standard: Mon Nov 16 | 4.0" TFT, 480×320 (used as 320×480 portrait), 65K colors<br>SPI interface, ST7796S driver<br>8 pins used: VCC, GND, CS, RESET, DC/RS, SDI (MOSI), SCK, LED | 8 female-to-female jumpers to the Zero header: VCC→pin 1 (3.3V), GND→20, CS→24, RESET→13, DC→22, MOSI→19, SCK→23, LED→17<br>Screw into the lid by its 4 corner holes | Touch, SD slot and MISO pins not used. Confirm with the seller whether VCC is 3.3V or 5V; start at 3.3V. |
| 1.3 | Storage | [SanDisk Ultra 32 GB microSDHC, A1](https://www.amazon.com/dp/B08GY9NYRM) · SDSQUA4-032G | 1 EA | $21.33 → $21.33<br>Amazon | In stock<br>Free: Wed Nov 18 | 32 GB, UHS-I, A1 (fast small reads and writes) | Flash Raspberry Pi OS Lite with Raspberry Pi Imager<br>Insert into the Zero's card slot | Any A1-rated 16–32 GB card works. |

### 2.0 Base: control PCB assembly

| Item | Component | Model (link) · MFR part # | Qty / UOM | Price: pack → per device | Shipping time | Specs | Installation | Notes / Ref des |
|---|---|---|---|---|---|---|---|---|
| 2.1 | Control PCB | 2-layer board, JLCPCB or PCBWay | 5 boards (min. order), 1 used | $10–25 → $2–5<br>(estimate) | About 1–3 weeks for fab plus shipping (estimate) | 2-layer FR-4, pastel solder mask<br>MX switch footprints with LED cutouts<br>Test points, 0 Ω solder jumpers, spare-pin header | Designed in KiCad from the working breadboard<br>ERC, DRC and an outside review before ordering | PCB1. Extra boards are spares for rework. |
| 2.2 | Microcontroller | [Raspberry Pi Pico 2, no headers](https://www.digikey.com/en/products/detail/raspberry-pi/SC1631/24627142) · Raspberry Pi SC1631 | 1 EA | $6.12 → $6.12<br>DigiKey | In stock (19,421) | RP2350, dual Cortex-M33 at 150 MHz, 520 KB SRAM, 4 MB flash<br>26 GPIO: 15 used (11 keys, 1 LED data, 3 audio)<br>PIO blocks for LEDs and I2S audio | Solder flat onto the PCB by its castellated edges<br>Connects to the Zero over USB as a keyboard + serial port | U1. Wire keys active-low with internal pull-ups: the RP2350 E9 erratum affects internal pull-downs. |
| 2.3 | Key switches | [Blue clicky MX-style switches, 3-pin, transparent housing (30-pack)](https://www.amazon.com/dp/B0FM88HSCL) · Amazon B0FM88HSCL | 11 EA (30-pack) | $6.99 → $2.56<br>Amazon | In stock<br>Prime: Thu Nov 12<br>Free standard: Mon Nov 16 | Clicky tactile, MX cross stem<br>3-pin PCB mount<br>Transparent housing lets the LED underneath shine through | Snap into 14 mm square holes in the case top (about 1.5 mm thick so the clips lock)<br>Solder the 2 pins to the PCB | SW1–SW11: Up, Down, Left, Right, OK, Back, Fav, Try-on, Style, Comfort −, Comfort + |
| 2.4 | Keycaps | [Adafruit clear keycaps for MX switches, 12-pack](https://www.digikey.com/en/products/detail/adafruit-industries-llc/5068/14617348) · Adafruit 5068 | 11 EA (12-pack) | $6.95 → $6.37<br>DigiKey | In stock (47) | Clear, DSA profile (flat, symmetric), 1U<br>Fits MX cross stems | Press onto each switch after soldering | The Amazon switch + keycap kit the doc used to list is currently unavailable. |
| 2.5 | RGB LEDs | [Adafruit NeoPixel reverse-mount LEDs, SK6812-E, 10-pack](https://www.digikey.com/en/products/detail/adafruit-industries-llc/4960/14302512) · Adafruit 4960 | 11 EA (2 × 10-pack) | $5.90 → $3.25<br>DigiKey | In stock (428) | SK6812-E addressable RGB, 5V<br>Built-in constant-current driver, no resistor per LED<br>3.1 × 2.7 × 1.7 mm | LED body sits in a cutout in the PCB under each switch and shines up through it<br>Hand-solder the long pads at low iron temperature | D1–D11, chained. 9 spares because they're small and heat-sensitive. |
| 2.6 | Level shifter | [TI SN74AHCT125N, quad buffer, DIP-14](https://www.digikey.com/en/products/detail/texas-instruments/SN74AHCT125N/375798) · SN74AHCT125N | 1 EA (2 bought) | $1.90 → $0.95<br>DigiKey Marketplace | In stock (492)<br>Ships separately from the Marketplace seller | 5V supply, TTL inputs read the Pico's 3.3V as high<br>Outputs a full 5V signal | Pico GPIO → 1A, 1Y → R1 → D1 data in<br>Tie 1OE low; tie unused inputs to GND and their OE pins high | U2. SK6812 needs at least 3.5V for "high" at 5V, so the Pico can't drive it directly. 1 spare. |
| 2.7 | LED data resistor | [Stackpole CF14JT330R, 330 Ω](https://www.digikey.com/en/products/detail/stackpole-electronics-inc/CF14JT330R/1830338) · CF14JT330R | 1 EA (10 bought) | $0.27 → $0.03<br>DigiKey | In stock (262,298) | 330 Ω, ±5%, 1/4 W, carbon film, through-hole | In the LED data line, close to D1 | R1. Damps ringing and protects D1 if LED power drops while data is still sent. 10 cost less than 1. |
| 2.8 | Bulk capacitor | [Panasonic EEU-FR1C471, 470 µF 16V](https://www.digikey.com/en/products/detail/panasonic-industry/EEU-FR1C471/2433528) · EEU-FR1C471 | 1 EA | $0.71 → $0.71<br>DigiKey | In stock (739) | 470 µF, 16V, aluminum electrolytic, radial<br>Polarized (stripe marks −) | Across the LED 5V and GND near D1 | C1. Smooths 5V dips when the LEDs change color. |
| 2.9 | Decoupling capacitors | [Vishay K104K15X7RF5TL2, 0.1 µF 50V](https://www.digikey.com/en/products/detail/vishay-beyschlag-draloric-bc-components/K104K15X7RF5TL2/286706) · K104K15X7RF5TL2 | 12 EA | $2.04 → $2.04<br>DigiKey ($0.17 each at 10+) | In stock | 0.1 µF, ±10%, 50V, X7R ceramic, radial<br>Not polarized | One beside each LED (11) and one at U2 (1) | C2–C13. Filters power-pin noise. |
| 2.10 | Audio amp | [Adafruit MAX98357A I2S amp breakout](https://www.digikey.com/en/products/detail/adafruit-industries-llc/3006/6058477) · Adafruit 3006 | 1 EA | $5.95 → $5.95<br>DigiKey | In stock (3,896) | I2S class-D, 2.7–5.5V supply, 3.3V logic OK<br>1.8 W into 8 Ω at 5V, 9 dB default gain<br>Thermal and over-current shutdown | Solder the included header; mount on the PCB<br>VIN from 5V (USB VBUS), not the Pico's 3.3V<br>BCLK, LRC, DIN to 3 Pico GPIO | U3. Speaker screws into the board's terminal block. |
| 2.11 | Speaker | [Taoglas SPKM.28.8.A, 28 mm](https://www.digikey.com/en/products/detail/taoglas-limited/SPKM-28-8-A/16496639) · SPKM.28.8.A | 1 EA | $2.43 → $2.43<br>DigiKey | In stock (1,035) | 8 Ω, 1 W rated (1.5 W max), 89 dB<br>28 mm diameter, 5.1 mm tall, wire leads | Wire leads into the amp's terminal block, no soldering<br>Add grille holes in the case | LS1. The amp can push 1.8 W, so cap the volume in firmware. |
| 2.12 | Spare-pin header | [Sullins PREC040SAAN-RC, 1×40, 2.54 mm](https://www.digikey.com/en/products/detail/sullins-connector-solutions/PREC040SAAN-RC/2774814) · PREC040SAAN-RC | 13 pins (40-pin strip) | $0.49 → $0.16<br>DigiKey | In stock (39,460) | Breakaway male header, through-hole | Breaks out the 11 unused Pico pins + 3.3V + GND | J1. Lets you rewire without ordering a new PCB. |
| 2.13 | Solder jumpers | KiCad footprint SolderJumper_2_Bridged | 12 | $0 (part of the PCB) | n/a | Two pads joined by a thin copper trace | On each key line and the LED data line<br>Cut to disconnect, add solder to reconnect | JP1–JP12 |

### 3.0 Power and cabling

| Item | Component | Model (link) · MFR part # | Qty / UOM | Price: pack → per device | Shipping time | Specs | Installation | Notes |
|---|---|---|---|---|---|---|---|---|
| 3.1 | Power bank | [Miady 5000 mAh power bank (2-pack)](https://www.amazon.com/dp/B08T8TDS8S) · Amazon B08T8TDS8S | 1 EA | Owned ($16.99 per 2-pack, about $8.50 each) | Owned | USB-A output 5V / 2.4A, USB-C in/out<br>18.5 Wh, 92 × 64 × 10 mm | Sits in the base<br>Leave an opening for its USB-C charging port | Deck draws about 0.6–1.2 A (estimate), so roughly 2.5–5 hours per charge. |
| 3.2 | On/off cable | [Adafruit USB-A to micro-B cable with switch, 1.5 m](https://www.digikey.com/en/products/detail/adafruit-industries-llc/2379/5774324) · Adafruit 2379 | 1 EA | $5.95 → $5.95<br>DigiKey | In stock (25) | Inline on/off switch, power only<br>1.5 m long | Power bank USB-A → cable → Zero micro-USB PWR IN<br>Runs through the hinge; coil the extra length in the base | Use the app's shutdown option before switching off so the SD card isn't corrupted. |
| 3.3 | USB data cable | Short USB-A to micro-B data cable + the kit's OTG adapter | 1 EA | Owned | Owned | Must carry data, not charge-only | Pico → OTG adapter → Zero micro-USB data port<br>Runs through the hinge | Also powers the control PCB from the Zero. |

### 4.0 Enclosure and mounting

| Item | Component | Model (link) · MFR part # | Qty / UOM | Price: pack → per device | Shipping time | Specs | Installation | Notes |
|---|---|---|---|---|---|---|---|---|
| 4.1 | Case | Hinged box prototype, then a 3D-printed shell (Onshape or Fusion) | 1 | $5–20 (estimate) | n/a | Lid: screen + Zero. Base: PCB, power bank, speaker<br>Case top is also the switch plate | Hinge slot fits 2 micro-USB cables (data + power)<br>Design after breadboarding, around measured parts | Print at a library, makerspace or print service. |
| 4.2 | Standoffs and screws | [iUniker M2.5 brass standoff kit, 134 pcs](https://www.amazon.com/dp/B0F6MNBQVL) · Amazon B0F6MNBQVL | About 8 pcs (134-pc kit) | $9.99 → about $0.60<br>Amazon | In stock<br>Prime: Thu Nov 12<br>Free standard: Mon Nov 16 | M2.5 standoffs, screws and nuts | Mounts the Zero (M2.5 holes) and the control PCB (give it M2.5 holes) | Screen corner screws: measure its holes when it arrives. |

### 5.0 Prototyping parts (not in the finished deck)

| Item | Component | Model (link) · MFR part # | Qty / UOM | Price | Shipping time | Specs | Use |
|---|---|---|---|---|---|---|---|
| 5.1 | Breadboard Pico | [Raspberry Pi Pico 2 H, headers attached](https://www.digikey.com/en/products/detail/raspberry-pi/SC1632/26241102) · Raspberry Pi SC1632 | 1 EA | $6.00<br>DigiKey | In stock (5,587) | Same RP2350 as U1, with headers | Breadboard and firmware testing before the PCB arrives |
| 5.2 | Jumper wires | [Adafruit female-to-female jumpers, 40 × 6"](https://www.digikey.com/en/products/detail/adafruit-industries-llc/266/5629427) · Adafruit 266 | 1 pack | $3.95<br>DigiKey | In stock (43) | 40 wires, 6", female on both ends | Screen-to-Zero wiring (8 wires); header-to-header connections |
| 5.3 | Breadboard | Solderless breadboard | 1 | Owned | Owned | | Pico, a few switches, level shifter, amp |