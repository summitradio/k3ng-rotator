#Basic Schematic

![](https://radioartisan.files.wordpress.com/2011/03/k3ng_arduino_rotator_controller_2011092801.png)

Note: Refer to the pin numbers on the inside of the Arduino component outline (i.e. D1, D2, A0, A1, etc.) and not the numbers on the outside of it (1, 2, 3...).

The schematic above shows a basic setup supporting a 4 bit interface LCD, azimuth and elevation voltage (FEATURE_AZ_POSITION_POTENTIOMETER and FEATURE_EL_POSITION_POTENTIOMETER) inputs, manual buttons, and a single variable speed voltage output.  Additional controls and options such as an azimuth present potentiometer, azimuth and elevation preset rotary encoders, and brake control lines can be added as needed if the appropriate pins are chosen and set in code at compilation time.  If using with an azimuth-only rotator, all components related to elevation can be omitted.  So, again, keep in mind the above schematic is a very basic unit that will work for most applications and additional features will require additional components.

The buttons, LCD, and speed potentiometer cab be omitted if a simple computer to rotator interface is desired.  If more sophisticated position sensors are desired, they can be connected to the Arduino pines based on settings within [rotator_pins.h](https://github.com/k3ng/k3ng_rotator_controller/blob/master/rotator_pins.h).  I2C devices are merely connected to the I2C pins of the Arduino.  The exact pins vary between Arduino models, and additional information in .