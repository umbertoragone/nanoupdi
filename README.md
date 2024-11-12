# NanoUPDI
The smallest USB Type-C Serial UPDI programmer for your projects.

<p align=center>
  <img src="/images/nanoupdi_3.jpg?raw=true" alt="NanoUPDI programmer front" width=400 />
  <img src="/images/nanoupdi_4.jpg?raw=true" alt="NanoUPDI programmer back" width=400 />
</p>

## What is UPDI?
UPDI is an [Atmel/Microchip](https://www.microchip.com) proprietary programming interface, much like JTAG/SWD used in ARM chips with CMSIS-DAP tools. It's the default programming mode for some of the new AVR microcontrollers we like, namely the ATTINY212, ATTINY412, ATTINY414 and ATTINY1614. Also! It only requires one pin to use: nice.

## Features
- **CH340E USB to Serial converter**: A compact version of the well-known WCH CH340x series, which doesn't require an external crystal oscillator.
- **Compact Form Factor**: At only 10 x 22 mm (excluding header pins), it is the smallest serial UPDI programmer on the market.
- **VCC Voltage Selector**: Easily switch between 3.3V (3V3) and 5V logic voltages with a simple flick of a switch.
- **USB 2.0 speed**: Compatible with any USB Type-C cable that supports USB 2.0 (480 Mbps) speeds or greater. The reversible USB Type-C connector allows the cable to be plugged in either orientation, maintaining full functionality.
- **Status LEDs**: Includes a green LED for power (PWR) and a red LED that blinks during data transfer (TX).

## Installation and how to use
No installation required, it is Plug&Play with the majority of operating systems since the CH340x is a commonly used USB-to-serial converter.
If you use `avrdude` to program your UPDI compatible AVR microcontrollers, you simply need to specify `serialupdi` as the programmer:

```bash
avrdude -c serialupdi -p t414 -P /dev/tty.usbserial-10
```

Make sure to specify the correct serial device: on Linux devices, NanoUPDI might show up as `/dev/ttyUSBX`, while on MacOS it might show as `/dev/tty.usbserial-XX`.

## Gerber files
If you want to fabricate your own PCBs from a PCB manufacturer of your choice, you can go ahead and download the `Gerber.zip` file from this repository. Upload it or send it to the PCB fabrication house and select the following specifications (if not already filled out):
- **Layers**: 2
- **PCB Thickness**: 1.6 mm
- **PCB Color**: any (green is usually cheaper and faster to produce, but black looks nicer)
- **Outer Copper Weight**: 1 oz
- **Via Covering**: Tented
- **Mark on PCB**: Order Number(Specify Position) or Remove Mark for a bit extra (JLCPCB specific)

## BOM and assembly
Included in this repository is the HTML BOM to help you in the assembly/soldering process after you received your PCBs. Also, here is the list of components you will have to source and solder yourself:

| Reference(s) | Value                   | Footprint                       | LCSC Part #                                                   | Aliexpress Link | Qty |
|--------------|-------------------------|---------------------------------|---------------------------------------------------------------|-----------------|-----|
| C1, C3, C4   | 100nF 50V 10% X7R       | C_0603_1608Metric               | [C14663](https://www.lcsc.com/product-detail/C14663.html)     |                 | 3   |
| C5, C6       | 10uF 10V 10% X7R        | C_0805_2012Metric               | [C237493](https://www.lcsc.com/product-detail/C237493.html)   |                 | 2   |
| R1, R2       | 5k1 1%                  | R_0402_1005Metric               | [C25905](https://www.lcsc.com/product-detail/C25905.html)     |                 | 2   |
| R3, R6       | 470R 1%                 | R_0402_1005Metric               | [C25117](https://www.lcsc.com/product-detail/C25117.html)     |                 | 2   |
| R4           | 0R 1%                   | R_0603_1608Metric               | [C21189](https://www.lcsc.com/product-detail/C21189.html)     |                 | 1   |
| R5           | 1k 1%                   | R_0402_1005Metric               | [C11702](https://www.lcsc.com/product-detail/C11702.html)     |                 | 1   |
| D1           | 1N4148                  | D_SOD-523                       | [C727112](https://www.lcsc.com/product-detail/C727112.html)   |                 | 1   |
| D2           | EMERALD/GREEN           | LED_0603_1608Metric             | [C965804](https://www.lcsc.com/product-detail/C965804.html)   |                 | 1   |
| D3           | RED                     | LED_0603_1608Metric             | [C965799](https://www.lcsc.com/product-detail/C965799.html)   |                 | 1   |
| U1           | CH340E                  | MSOP-10_3x3mm_P0.5mm            | [C99652](https://www.lcsc.com/product-detail/C99652.html)     |                 | 1   |
| SW1          | MSK12C02                | MSK12C02                        | [C431540](https://www.lcsc.com/product-detail/C431540.html)   |                 | 1   |
| FB1          | 220R @ 100MHz           | L_0805_2012Metric               | [C85840](https://www.lcsc.com/product-detail/C85840.html)     |                 | 1   |
| USB1         | USB_C_Receptacle_USB2.0 | TYPE-C-31-M-12                  | [C2988369](https://www.lcsc.com/product-detail/C2988369.html) |                 | 1   |
| VREG1        | AP2112K-3.3             | SOT-23-5                        | [C51118](https://www.lcsc.com/product-detail/C51118.html)     |                 | 1   |
| J1           | Conn_01x03              | PinHeader_1x03_P2.54mm_Vertical | [C492411](https://www.lcsc.com/product-detail/C492411.html)   |                 | 1   |
