# ahrs-can-adapter

KiCad design for a CAN adapter to a Dronecad flight board. The MCU is a
stm32f107rbt6.

## Changes

- Rev A
  Original

## Firmware

[Firmware](https://github.com/gpgreen/ahrs-can-adapter)

## Connections to Segger JTAG

I have put test points on the board, so that pogo pins can be used to program
the MCU.

[jlink web page](https://www.segger.com/products/debug-probes/j-link/technology/interface-description/)
```
**** 20 Pin connector for JTAG
                -------
    VTref      1|*   *|2 NC
    nTRST      3|*   *|4 GND
    TDI        5|*   *|6 GND
    TMS        7|*   *|8 GND
    TCK        9|*   *|10 GND
    RTCK      11|*   *|12 GND
    TDO       13|*   *|14 GND
    RESET     15|*   *|16 GND*
    DBGRQ     17|*   *|18 GND*
    5V Supply 19|*   *|20 GND*
                -------
```
From a 20pin JTAG connector, run wires to the following test pads to connect a debugger:
```
VTRef 1  <-> 3V3
SWDIO 7  <-> SWD
SWCLK 9  <-> SWC
RESET 15 <-> RST
GND   4  <-> GND
```

## Running SEGGER JLink

Run the JLink GDB server via the following:
```
JLinkGDBServer -if SWD -device STM32F103CB
```

GDB can be connected via the following:
```
gdb-multiarch --command=jlink-stm32.gdb target/thumbv7m/debug/main
```

## Running ocd
```
openocd -f interface/stlink-v3.cfg -f target/stm32f1x.cfg
```

## Credits

as always, thanks for the good work
- [Adafruit](https://www.adafruit.com)

## License

Licensed under

- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)
