
## Summary

This project is an SOC (System on a Chip) coded in VHDL and implemented for the Lattice iCE40-hx8k dev board. The SOC contains the following components: 6811 CPU + UART + Timer + I/O Ports

## Required Hardware

* Lattice iCE40-hx8k dev board (can be ordered online at www.latticesemi.com)
* USB-to-Serial 3.3V adapter (can be ordered from eBay)
* misc USB cables and wires for connecting the USB-to-Serial adapter

NOTE: Make sure the USB-to-serial adapter is a 3.3V version. Some adapters have 5V interface signals which could damage your iCE40-hx8k dev board.

## Tools

* IceCube2 (from Lattice Semiconductor) was used for synthesis and FPGA Routing.
* Icestorm (https:/github.com/cliffordwolf/icestorm) was used for programming.


## Build Flow

I used the Lattice IceCube2 software to generate the SOC_bitmap.bin programming file and then I used this command line "iceprog SOC_bitmap.bin" the program the iCE40-hx8k dev board over the USB cable (iceprog is part of the icestorm tool suite).

## Console Interface

I used the minicom program (on Ubuntu Linux) as a console to communicate with the 6811 SOC over the USB-to-Serial connection. Configure minicom using the command line "minicom -s" to configure the serial port for ttyUSB0 and turn of the hardware handshaking. There are probably other alternatives to minicom. Any ANSI terminal-emulator program should work for this application.

## Pinout

The iCE40 pins are defined as follows:
```
UART_RXD   G1 -pullup yes
UART_TXD   G2
PORTA[0]   B5
PORTA[1]   B4
PORTA[2]   A2
PORTA[3]   A1
PORTA[4]   C5
PORTA[5]   C4
PORTA[6]   B3
PORTA[7]   C3
RESET      N3 -pullup yes
CLK        J3 -pullup yes
```

## 6811 CPU Background Info

The MC6811 is an eight-bit microprocessor that was introduced by Motorola in 1985. It has two 8-bit accumulators (A&B)that can be combined into a single 16-bit register (D). It also features two 16-bit index registers (X&Y) and a stack pointer (SP), which allows for very flexible addressing modes. The 6811 can trace its lineage back to the earlier 6800 and the 6811 is upwards source-code (but not machine code) compatible with the 6800. Many new instructions were added to the 6811 including bit test instructions (similar to those on the 6805) and multiply and divide instructions. There were many versions of the 6811 produced with different I/O peripheral options. This SOC implements the core 6811 CPU and does not attempt to emulate any specific 6811 chip I/O options.


## Contributors

* Scott L Baker - SOC design

## License

See the **LICENSE** file in this repository
