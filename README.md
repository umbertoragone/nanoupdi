# NanoUPDI
The smallest USB Type-C Serial UPDI programmer for your projects. **Available for purchase on my [Tindie store](https://www.tindie.com/products/ragone/nanoupdi/)!**

<img src="/images/nanoupdi_3.jpg?raw=true" alt="NanoUPDI programmer front" width=400 /> <img src="/images/nanoupdi_4.jpg?raw=true" alt="NanoUPDI programmer back" width=400 />

## What is UPDI?
UPDI is a proprietary programming interface developed by [Atmel/Microchip](https://www.microchip.com), similar to the JTAG/SWD interfaces used for ARM microcontrollers. It's the default programming interface for several newer AVR microcontrollers, including models like the ATTINY212, ATTINY412, ATTINY414, etc. It only requires a single pin for programming, so it's more convenient and efficient.

## Features
- **CH340E/CH340X USB to Serial converter**: A compact version of the well-known WCH CH340x series, which doesn't require an external crystal oscillator.
- **Compact Form Factor**: At only 10 x 22 mm (excluding header pins), it is the smallest serial UPDI programmer on the market.
- **VCC Voltage Selector**: Easily switch between 3.3V (3V3) and 5V logic voltages with a simple flick of a switch.
- **USB Type-C**: Compatible with any USB Type-C cable that supports both power and data (USB 2.0 or greater). The reversible USB Type-C connector allows the cable to be plugged in either orientation, maintaining full functionality (data and power).
- **2.54mm Pitch Pin Header**: Designed for right-angle (horizontal) pin headers with a 0.1" (2.54mm) pitch pin headers (breadboard compatible), it also allows for custom wires or connectors to be soldered based on your needs.
- **Status LEDs**: Includes a green LED for power (PWR) and a red LED that blinks during data transfer (TX).
- Inspired by [Stefan Wagner](https://github.com/wagiminator)'s [SerialUPDI Programmer](https://github.com/wagiminator/AVR-Programmer/tree/master/SerialUPDI_Programmer).

## Installation and how to use
No installation required, it is Plug&Play with the majority of operating systems since the CH340x is a commonly used USB-to-serial converter.

### Avrdude
If you use `avrdude` to program your UPDI compatible AVR microcontrollers, you simply need to specify `serialupdi` as the programmer:

```bash
avrdude -c serialupdi -p t414 -P /dev/tty.usbserial-10
```

Make sure to specify the correct serial device: on Linux devices, NanoUPDI might show up as `/dev/ttyUSBX`, while on MacOS it might show as `/dev/tty.usbserial-XX`.

### Arduino IDE
To use NanoUPDI with the Arduino IDE, first install the [megaTinyCore board support package](https://github.com/SpenceKonde/megaTinyCore), then choose **Serial UPDI** as the programmer in the dropdown menu.

## Kicad files
If you want to open and modify the original project in Kicad 8 (>=8.0.6), you can find both the `.kicad_sch` and `.kicad_pcb` files in the `kicad` folder in this repository. I recommend you use the latest Kicad 8 version available for better compatibility.

## Gerber files
If you want to fabricate your own PCBs from a PCB manufacturer of your choice, you can go ahead and download the `Gerber-v2.x.zip` file from the `gerber` folder in this repository. Upload it or send it to the PCB fabrication house and select the following specifications (if not already filled out):
- **Layers**: 2
- **PCB Thickness**: 1.6 mm
- **PCB Color**: any (green is usually cheaper and faster to produce, but black looks nicer)
- **Outer Copper Weight**: 1 oz
- **Via Covering**: Tented
- **Mark on PCB**: Remove Mark (JLCPCB specific, now free of charge)

## BOM and assembly
Included in this repository is the HTML BOM to help you in the assembly/soldering process after you received your PCBs. Also, here is the list of components you will have to source and solder yourself:

| Reference(s) | Value                   | Footprint                       | LCSC Part #                                                   | Qty |
|--------------|-------------------------|---------------------------------|---------------------------------------------------------------|-----|
| C1, C4, C5   | 100nF 50V 10% X7R       | C_0603_1608Metric               | [C14663](https://www.lcsc.com/product-detail/C14663.html)     | 3   |
| C2, C3       | 10uF 10V 10% X7R        | C_0805_2012Metric               | [C237493](https://www.lcsc.com/product-detail/C237493.html)   | 2   |
| R1, R2       | 5k1 1%                  | R_0402_1005Metric               | [C25905](https://www.lcsc.com/product-detail/C25905.html)     | 2   |
| R3, R6       | 470R 1%                 | R_0402_1005Metric               | [C25117](https://www.lcsc.com/product-detail/C25117.html)     | 2   |
| R4           | 0R 1%                   | R_0603_1608Metric               | [C21189](https://www.lcsc.com/product-detail/C21189.html)     | 1   |
| R5           | 1k 1%                   | R_0402_1005Metric               | [C11702](https://www.lcsc.com/product-detail/C11702.html)     | 1   |
| D1           | 1N4148                  | D_SOD-523                       | [C727112](https://www.lcsc.com/product-detail/C727112.html)   | 1   |
| D2           | EMERALD/GREEN           | LED_0603_1608Metric             | [C965804](https://www.lcsc.com/product-detail/C965804.html)   | 1   |
| D3           | RED                     | LED_0603_1608Metric             | [C965799](https://www.lcsc.com/product-detail/C965799.html)   | 1   |
| U1           | CH340E                  | MSOP-10_3x3mm_P0.5mm            | [C99652](https://www.lcsc.com/product-detail/C99652.html)     | 1   |
| SW1          | MSK12C02                | MSK12C02                        | [C431540](https://www.lcsc.com/product-detail/C431540.html)   | 1   |
| FB1          | 220R @ 100MHz           | L_0805_2012Metric               | [C85840](https://www.lcsc.com/product-detail/C85840.html)     | 1   |
| USB1         | USB_C_Receptacle_USB2.0 | TYPE-C-31-M-12                  | [C2988369](https://www.lcsc.com/product-detail/C2988369.html) | 1   |
| VREG1        | AP2112K-3.3             | SOT-23-5                        | [C51118](https://www.lcsc.com/product-detail/C51118.html)     | 1   |
| J1           | Conn_01x03              | PinHeader_1x03_P2.54mm_Vertical | [C92159](https://www.lcsc.com/product-detail/C92159.html)     | 1   |

## Component substitutions
- **U1**: in case the CH340E is not available, the [CH340X](https://www.lcsc.com/product-detail/C3035748.html) should be a drop in replacement for the [CH340E](https://www.lcsc.com/product-detail/C99652.html): same footprint, same pinout and basically the same function—at least in the scope of this UPDI programmer.
- **FB1**: you can use a 0R 0805 resistor or solder a jumper wire in place to make it work. The ferrite bead is there to reduce possible noise from the VBUS (5V) line generated by your computer, so it is generally recommended for stability, but not critical. If you leave it empty, the rest of the board will have no power.
- **C1**: it is a decoupling capacitor for VBUS, marked as "do not place", since it is redundant. In fact, on the boards I sell on my [Tindie store]([url](https://www.tindie.com/products/ragone/nanoupdi/)), it is not populated by default.
- **D1**: it can be swapped with a 1k 0402 resistor (loopback resistor between RX and TX). Both solutions will work the same.

## Prebuilt option
If you're looking for a NanoUPDI programmer that's already assembled and ready to go, I offer a prebuilt option that's perfect for those who want a plug-and-play solution without the hassle of sourcing and assembling components. Each unit is handcrafted and fully tested before shipping. **[Check it out on my Tindie store](https://www.tindie.com/products/ragone/nanoupdi/)**.
