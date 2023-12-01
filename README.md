# USB PTT Cable

![USB PTT Cable](https://github.com/UT8IFG/PTT-USB-Cable/raw/main/photo/usb-ptt-cable.jpg)

The USB PTT Cable is a simple galvanically isolated USB-PTT interface for amateur radio equipment. It was originally designed as a USB-PTT interface for the [PA Controller](https://vhfdesign.com/pas/pa-controller.html) (manufactured by VHFDesing.com) to allow operation in digital modes. 

The basic idea is to use a plastic housing and a 4-wire cable of USB-UART converters sold on Aliexpress and other marketplaces as parts of the USB PTT Cable. This makes it easier and cheaper to build the device at home.

The USB PTT Cable is based on a CP2102 USB-UART bridge chip and its output is galvanically isolated from the USB interface by an optocoupler. It also has a two-color LED for status indication: green for standby (RX) and red for transmit (TX).

PTT is controlled by the RTS or DTR signal of the virtual COM port. The control signal can be selected by a solder jumper. By default, the RTS signal is used. 

The device's output circuit has a current limiting resistor to protect the optocoupler transistor, so the output cannot drive a large load such as a relay coil. To increase the output current, the current limiting resistor must be short-circuited with a solder jumper. In this case the optocoupler transistor will be directly connected to the output connector.

## PCB
The board is designed for hand soldering and contains 0805 size passive SMD components. The most difficult part may be soldering the CP2102 chip in the QFN-28 package.

The minimum hole diameter is 0.3mm to reduce the final production cost in some PCB factories.

The board layout allows you to make the PCB at home using the TTM (Toner Transfer Method). In this case, it will be more convenient to drill a single large hole on the ground polygon of the CP2102 chip. The board layout also has a via under the optocoupler package.

<img src="https://github.com/UT8IFG/PTT-USB-Cable/raw/main/photo/pcb-assembled-top.jpg" width="49%"/> <img src="https://github.com/UT8IFG/PTT-USB-Cable/raw/main/photo/pcb-assembled-bottom.jpg" width="49%"/>

## Why CP2102?

The choice of USB-UART bridge IC for the USB PTT Cable was based on observing the behavior of the RTS and DTR signals during PC boot, PC shutdown, and IC initialization after connection to a USB port.

The following chips were tested: CH340E, PL2302HX, PL2303TA, FT323RL and CP2102. A PC was running Windows 10 and Debain Linux operating systems.

As a result, only the CP2102 chip did not have a phantom triggers on the RTS and DTR outputs during PC boot, shutdown, and connecting the bridge IC to a USB port. However, a short phantom trigger is observed during WSJT-X startup.

## Driver installation

### Linux

The CP210х driver has been distributed as part of the Linux kernel since v2.6.12. 

### Windows 10 & Windows 11

Windows 10 (version 1803 and later) and Windows 11 require manual installation of the Virtual COM Port Universal driver provided by Silicon Labs.

You can find the latest WCP210x Universal Windows Driver at this [link](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=downloads).

Older versions of Windows automatically install the driver through Windows Update.

### MacOS X

For computers running MacOS X 10.11 or greater, the CP210x VCP Mac OSX Driver is available [here](https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=downloads).

### Other

Silabs also provides drivers for other operating systems such as Android or WinCE.

