# Details on Interfacing with Various Commercial Controller Units

[This guide from EA4TX](http://ea4tx.com/PDF/QuickInstallationGuideRCI-USB.pdf) can provide useful information on interfacing with rotator control units that lack an external control port.

## Yaesu G1000DXA

Interface to the External Control port on the back.

[Manual with schematic](https://www.yaesu.com/downloadFile.cfm?FileID=685&FileCatID=155&FileName=G%2D800%5FG%2D1000%5FG%2D2800%5FDXA%5FOpMan.pdf&FileContentType=application%2Fpdf)

Pin

1. ground to go R (CW) - relay/transistor switching from Arduino cw pin

1. ground to go L (CCW) - relay/transistor switching from Arduino cw pin

1. speed control - tie to +5V for max speed or interface to Arduino azimuth_speed_voltage pin with cap and resistor per project schematic

1. voltage for azimuth heading - goes into Arduino rotator_analog_az pin

1. ground

1. +5V out (can tie to pin 3 for max speed)


## Yaesu G-450XL

[Schematic](http://www.radiomanual.info/schemi/ACC_rotator/Yaesu_G-450XL_user.pdf)

There is no external control port to directly interface with.  Consult the [EA4TX guide](http://ea4tx.com/PDF/QuickInstallationGuideRCI-USB.pdf).

## Yaesu G-550