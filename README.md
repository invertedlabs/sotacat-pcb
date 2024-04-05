# SOTAcat PCB

This project creates a SOTAcat PCB designed in [KiCad](https://www.kicad.org) and compatible with Brian AB6D's [SOTAcat](https://github.com/SOTAmat/SOTAcat) and [SOTAMAT](https://sotamat.com/) ("SOTA-Mate") web service and software. Brian provides a cloud service and iOS and Android which can interface with SOTAcat hardware to command an Elecraft KX2 or KX3 to transmit SOTA or POTA spots from the field via the FT8 spotting networks.  [The SOTAcat software](https://github.com/SOTAmat/) by Brian and Jeff KC6X also has other great features like a web interface that polls SOTA and POTA spots from their respective databases and commands the KX2 or KX3 to the spot frequency and mode with a single click.

This repository contains hardware files only. These files are available in zipped gerber form under "releases" which can be uploaded to PCB board manufacturers like [OshPark](https://www.oshpark.com), [JLCPCB](https://www.jlcpcb.com), or [PCBWay](https://www.pcbway.com) for quick turn around prototype-quantity builds.

# Attribution

A lot of folks from the SOTA community have contributed to this project.  For full attribution, see [the attribution list](https://github.com/SOTAmat/SOTAcat?tab=readme-ov-file#attribution) in the software repository. 

Specifically, this project wouldn't have been possible without the great SOTAmat software and original SOTAcat concetp by Brian Mathews AB6D, the SOTAcat software authored primarily by Brian and Jeff Kowalski KC6X, and timely feedback from Brian, Jeff, and Rex Vokey KE6MT during the design phase.

# Bill of Materials

A full BOM will be uploaded in due time, for now, refer to the schematic documents for build information, including part numbers for ordering from suppliers like [DigiKey](https://www.digikey.com) or [Mouser](https://www.mouser.com).

# Batteries

SOTAcat is a battery powered device. The battery is charged via a USB-C port.  Under the hood, a Seeeed XIAO ESP32-C3 board provides the USB port and battery charging circuitry. The battery is charged at 350mA, which limits the battery selection to batteries that can safely accept this amount of current. Most single-cell batteries above 300mAh will do fine given the bettery isn't allowed to overheat when charging. While many LiPo batteries are limited to 1C charging, test show that with a 300mAh battery the time spent above 1C is very brief, generally less than 10 minutes with a fully dead battery. Even so, the PCB can get warm during the charging process, and steps should be made to keep the battery and PCB cool during charging. This can be done by keeping the thermal paths between the PCB and the battery to a miniumum (e.g. don't tape them directly together without an insulating layer), and only charging an enclosed device at room temperature (<80 deg F, or <27 deg C).  

As with all LiPo batteries, *always monitor the device while charging* and don't leave the device charging in very hot conditions such as a car on a warm day.

More information will be forthcoming about which batteries we have tested and recommend. If purchasing a battery, connectors have been provided on v0.3 for both TinyCircuits batteries and KBT batteries. Check the schematic and layout for pinout information.

# Antenna

A wifi antenna needs to be attached to the XIAO ESP32-C3 module using the U.FL connector on that PCB (between the buttons).  Most XIAO ESP32-C3 purchases will include a flexible WiFI antenna. Other antennas have been tested and may be preferable in some cases (like when using a 3D printed case). Specifics TBD. 

# 3D Printed Cases

A number of 3D printed cases have been developed alongside this hardware by Justin K5EM (@poyting).  These files will also be posted and made available in time. If you want to build one before this happens, just reach out to @poynting.

# Changelog

v0.3 updates:
* Move the serial TX pin to the KXx interface to a pin without bootloader messages.
* Add transistor-based level conversion / inversion to the serial lines in both directions, improving robustness of the serial communications and removing the need for software serial port inversion.
* Add a battery monitor IC with a coulomb counter to improve the robustness of the battery level indicator. This is active even with the power switch off and causes ~5uA of battery drain. 
* Change form factor slightly by moving KXx plug to the corner of the board. This opens up room on the KX2 so that the SOTAcat doesn't block the key port in most cases.

v0.2 was a very quick turn PCB that translated AB6D's schematic to a PCB. v0.2 has some issues, notably that the TRRS R2 and Shield pins need to be tied together for working serial, and EFUSEs need to be set on the XIAO ESP32-C3 to limit the debug output on the pin used for KXx serial communications. With these changes, the device is very functional.

# Warranties (and lack thereof)

No warranties are expressed or implied by Jutin McAllister or InvertedLabs, LLC for the hardware in this repository. All files and information are provided as is, with all faults, and may not be suitable for any purpose.  While a best-faith effort has been taken to test these designs, they may cause damage to connected equipement. Some designs may be untested, and may not work as provided. Lithium batteries are inherently dangerous and may cause personal injury and/or damage to property, even when used correctly. Always monitor batteries during use, and store safely per the battery manufacturer's recommendations. Proceed with caution, use at your own risk.
