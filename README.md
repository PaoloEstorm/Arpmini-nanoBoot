# nanoBoot

This repository contains the source code for the USB HID-based bootloader for ATmegaXXU4 family of devices.

The name *nanoBoot* comes from the fact that the compiled source fits in the smallest available boot size on the ATMegaXXu4 devices, 256 words or 512 bytes. The code is based on Dean Camera's [LUFA](https://github.com/abcminiuser/lufa) USB implementation, but it is **EXTREMELY** streamlined, size-optimized and targeted for the [ATmega16U4](http://www.atmel.com/devices/atmega16u4.aspx) and [ATmega32u4](http://www.atmel.com/devices/atmega32u4.aspx) devices; I had to make quite a few hardware assumptions, mostly to the fuse settings related to clock configuration for things to be as compact as possible, but the code still allows for some flexibility.

In this fork of [nanoBoot](https://github.com/volium/nanoBoot), a rudimentary magic boot key is implemented (by setting register r27) to invoke the bootloader anytime without needing a hardware reset.

An example implementation of a function to jump directly to the bootloader is as follows:

      void EnterBootloader () {
         asm volatile(" ldi  r27, 1");  // Set register 27
         wdt_enable(WDTO_15MS);         // Reset
         while (1) {}                   // Wait reset
      }

# Install [Arpmini-Core](https://github.com/PaoloEstorm/Arpmini-Core) for a ready-to-use Arduino core
(the bootloader must be burned using an ISP)

For more information and detailed instructions, refer to the [original nanoBoot fork](https://github.com/volium/nanoBoot)

