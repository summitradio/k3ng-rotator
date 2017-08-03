Rotators can basically be divided into two major groups:
* DC rotated
* AC rotated

Most Yaesu G series rotators are DC based, usually with a voltage from 0 to 24 volts and the polarity of  the DC voltage is switched to provide clockwise and counter-clockwise rotation.  The G-5500 is one exception; it has a DC azimuth motor and an AC elevation motor.

Older rotators are most often AC operated.  Either dual motor windings will be used or a single winding with a switch phase shift capacitor provides alternate direction rotation.

Voltages are usually in the 12 to 30 VAC range, however **never assume and always use a voltmeter to measure actual voltages.  Also, be aware that capacitors such as the phase shift capacitor you find in control units (and any large capacitor for that matter) can hold a lethal charge and should be discharged before working on equipment.**

Often the most challenging part of interfacing to an older rotator is the azimuth potentiometer. These are often low resistance values, such as 25 to 100 ohms, originally intended to drive mechanical (needle) current meters in the control unit, and may not play well with a 5 volt supply voltage. The Arduino rotator control unit with `FEATURE_AZ_POSITION_POTENTIOMETER` and/or `FEATURE_EL_POSITION_POTENTIOMETER` requires a 0 to 5 volt azimuth and elevation voltage range to provide the best accuracy and precision.  Therefore, if using a low resistance potentiometer, an operation amplifier ("op amp") such as a 741 will be needed to transform the small voltage swing to a 0-5 volt swing.

If the rotator has a reostat (a variable resistor with two leads) or a potentiometer with a grounded wiper which essentially makes it a reostat, you can place a fixed resistor of equal value in series with the reostat and supply the fixed resistor with 10 volts to get the desired 5 volt swing.

Questions about interfacing to rotators should be posted on the [Radio Artisan Yahoo group](https://groups.yahoo.com/neo/groups/radioartisan/info), which is frequented by many radio amateurs who have built homebrew rotation systems or have interfaced to older rotators.
