# Wiring and Pin Layout

Microcontroller: **Raspberry Pi Pico 2 H** 


## Bus overview

| Bus | Pico pins | Devices |
|---|---|---|
| SPI1 | GP10 (SCK), GP11 (MOSI), GP12 (MISO) | RFM96W radio, BMP390 |
| SPI0 | GP18 (SCK), GP19 (MOSI), GP16 (MISO) | microSD card (on its own bus) |
| UART1 | GP4 (TX), GP5 (RX) | PA1010D GPS |
| I2C1 | GP26 (SDA), GP27 (SCL) | TMP117 (only device on the bus) |
| ADC3 (internal) | GP29 | Battery voltage (reads VSYS ÷ 3) |

## Pico 2 pin assignment

USB connector at the top.

| Pin | Name | Connected to | | Pin | Name | Connected to |
|---:|---|---|---|---:|---|---|
| 1 | GP0 | free | | 40 | VBUS | USB 5 V only, leave unconnected |
| 2 | GP1 | free | | 39 | VSYS | Battery + (via master switch and Schottky diode) |
| 3 | GND | PA1010D GND | | 38 | GND | Battery − / common ground |
| 4 | GP2 | free | | 37 | 3V3_EN | leave unconnected |
| 5 | GP3 | free | | 36 | 3V3(OUT) | VIN of all modules |
| 6 | GP4 | PA1010D RX (UART1 TX) | | 35 | ADC_VREF | — |
| 7 | GP5 | PA1010D TX (UART1 RX) | | 34 | GP28 | free (ADC2) |
| 8 | GND | — | | 33 | AGND | TMP117 GND |
| 9 | GP6 | PA1010D 1PPS (optional) | | 32 | GP27 | TMP117 SCL (I2C1) |
| 10 | GP7 | free | | 31 | GP26 | TMP117 SDA (I2C1) |
| 11 | GP8 | free | | 30 | RUN | optional reset button |
| 12 | GP9 | BMP390 CS | | 29 | GP22 | free |
| 13 | GND | BMP390 GND | | 28 | GND | — |
| 14 | GP10 | SPI1 SCK → RFM96W SCK, BMP390 SCK | | 27 | GP21 | free |
| 15 | GP11 | SPI1 MOSI → RFM96W MOSI, BMP390 SDI | | 26 | GP20 | free |
| 16 | GP12 | SPI1 MISO ← RFM96W MISO, BMP390 SDO | | 25 | GP19 | SPI0 MOSI → SD DI / CMD |
| 17 | GP13 | RFM96W CS | | 24 | GP18 | SPI0 SCK → SD CLK |
| 18 | GND | RFM96W GND | | 23 | GND | SD GND |
| 19 | GP14 | RFM96W RST | | 22 | GP17 | SD CS / D3 |
| 20 | GP15 | RFM96W G0 (DIO0 interrupt) | | 21 | GP16 | SPI0 MISO ← SD DO / D0 |

## Connections by module

### Adafruit RFM96W LoRa radio (433 MHz) — SPI1

The 433 MHz version is the RFM96W; the RFM95W is 868/915 MHz. Same pinout and library.

| Module pin | Pico pin |
|---|---|
| VIN | 3V3 (pin 36) |
| GND | GND (pin 18) |
| SCK | GP10 (pin 14) |
| MOSI | GP11 (pin 15) |
| MISO | GP12 (pin 16) |
| CS | GP13 (pin 17) |
| RST | GP14 (pin 19) |
| G0 | GP15 (pin 20) |
| EN | not connected |
| ANT | the antenna |


### Adafruit BMP390 pressure/temperature sensor — SPI1 (shared with radio)

| Module pin | Pico pin |
|---|---|
| VIN | 3V3 (pin 36) |
| GND | GND (pin 13) |
| SCK | GP10 (pin 14) |
| SDI | GP11 (pin 15) |
| SDO | GP12 (pin 16) |
| CS | GP9 (pin 12) |

### microSD card breakout — SPI0

| Module pin | Pico pin |
|---|---|
| 3V / VCC | 3V3 (pin 36) |
| GND | GND (pin 23) |
| CLK | GP18 (pin 24) |
| DI / CMD (MOSI) | GP19 (pin 25) |
| DO / D0 (MISO) | GP16 (pin 21) |
| CS / D3 | GP17 (pin 22) |


### Adafruit PA1010D GPS — UART1

| Module pin | Pico pin |
|---|---|
| VIN | 3V3 (pin 36) |
| GND | GND (pin 3) |
| TX | GP5 (pin 7) — Pico RX |
| RX | GP4 (pin 6) — Pico TX |
| 1PPS | GP6 (pin 9) — optional |
| SDA / SCL | not connected (using UART) |


### Adafruit TMP117 temperature sensor — I2C1

| Module pin | Pico pin |
|---|---|
| VIN | 3V3 (pin 36) |
| GND | AGND (pin 33) |
| SDA | GP26 (pin 31) |
| SCL | GP27 (pin 32) |
| INT, ADDR | not connected |

### 2000 mAh LiPo battery (JST connector)

| Battery lead | Connection |
|---|---|
| + (red) | VSYS (pin 39) |
| − (black) | GND (pin 38) |


## Power notes

- All modules are powered from the Pico's 3V3(OUT) rail (pin 36). Keep total 3V3 load under ~300 mA.
- The radio transmitting and SD card writes cause current peaks. If the Pico resets during transmission, move the RFM96W VIN to VSYS (its board accepts 3.3–6 V) and/or add a capacitor (e.g. 100 µF) near the radio.
- Battery voltage can be read on GP29 (ADC3), which measures VSYS ÷ 3.

## Free pins

GP0, GP1, GP2, GP3, GP7, GP8, GP20, GP21, GP22, GP28 (ADC2).