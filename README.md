This file describes how to install Klipper, a 3D printer firmware, on the GEEETECH A30Pro 3D printer.
This printer is equipped with a SMARTTO PCB featuring an STM32F103 microcontroller.

First, use the KIAUH installer to install KLIPPER, MOONRAKER, and MAINSAIL.
Instead of MAINSAIL, you can install OCTOPRINT or any other supported interface.

To compile the microcontroller code, run the following commands on your host device:

cd ~/klipper/
make menuconfig

For the SMARTTO board, select STM32F103, choose "No bootloader,"
and configure the serial connection (on USART1, PA10/PA9).

Next, run the following command:

make

To flash the firmware onto the Smartto board, use the command:

stm32flash -w out/klipper.bin -v -i rts,-dtr,dtr -b 115200 /dev/ttyUSB0

Flashing can be a bit tricky. First, connect the printer to the PC
using a USB cable. Then, use the following command to detect the connected device:

ls /dev/serial/by-id/*

This should return something like:

/dev/serial/by-id/usb-1a86_USB2.0-Serial-if00-port0

Next, power off the printer and disconnect the USB cable. Open the printer and place 
a jumper on the pins labeled BOOT0. Then, power on the printer, reconnect 
the USB cable, and use the previously mentioned command. For example:

stm32flash -w out/klipper.bin -v -i rts,-dtr,dtr -b 115200 /dev/serial/by-id/usb-1a86_USB2.0-Serial-if00-port0

If flashing does not work with the address /dev/serial/by-id/usb-1a86_USB2.0-Serial-if00-port0, try /dev/ttyUSB0 or /dev/ttyUSB1.





 




