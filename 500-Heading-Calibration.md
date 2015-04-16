## Yaesu GS-232 Emulation

On the serial interface, issue the O command and manually rotate the rotator to full counter-clockwise 180 degrees and send a carriage return.  Then issue the F command and manually rotate the rotator to full clockwise (270 degrees on a 450 degree rotator, or 180 degrees on a 360 degree rotator) and send a carriage return.

The elevation can be calibrated similarly with the O2 and F2 commands at 0 degrees and 180 degrees, respectively.

The calibration settings are written to non-volatile EEPROM memory.

## Easycom Emulation

The Easycom protocol does not have calibration commands like the Yaesu protocol, therefore you must manually configure these settings at compile time:

`#define ANALOG_AZ_FULL_CCW 4`

`#define ANALOG_AZ_FULL_CW 1009`

`#define ANALOG_EL_0_DEGREES 2`

`#define ANALOG_EL_MAX_ELEVATION 1018`

Another option is to compile with Yaesu GS-232 support, calibrate the unit, then recompile the code with Easycom support and upload it.

## Calibration Tables

If you have an azimuth or elevation sensor that is not linear and requires a calibration lookup table, that is provided in the code here:

`#define AZIMUTH_CALIBRATION_FROM_ARRAY {180,630} `

`#define AZIMUTH_CALIBRATION_TO_ARRAY {180,630}`

`#define ELEVATION_CALIBRATION_FROM_ARRAY {-180,0,180}`

`#define ELEVATION_CALIBRATION_TO_ARRAY {-180,0,180}`

To enable it, activate `FEATURE_AZIMUTH_CORRECTION` and/or `FEATURE_ELEVATION_CORRECTION` and configure the arrays above.  The from array is for the values coming from the sensor, and the to values are what you want to translate the values to.  Values that are between from values are extrapolated so there is no need to fill the arrays with every possible value, just end points and a reasonable number of points in between, depending on how nonlinear your sensor is and how much accuracy is needed.  Note that you must have an equal number of members in each from and to array.  The azimuth and elevation correction features apply to any sensor when activated.

## Manual Heading Calibration

The azimuth and elevation can be manually calibrated using the \A and \B commands, respectively. For example, to calibrate the azimuth:

\A175.3

This feature is not intended to be a replacement for calibration using the Yaesu GS-232 emulation O and F commands for the potentiometer sensors, but is intended for tweaking of calibration during a session.  For sensors like rotary encoders without a Z pulse and pulse inputs where the position is not absolute (not deterministically known at power up), the \A and \B commands may often needed to maintain accuracy.

## Heading Calibration for Incremental Shaft Encoders with Z Pulse

Recalibration of the system will occur automatically every time the rotor bearing passes thru the Z pulse bearing. The Z pulse bearing should be placed mechanically at an azimuth bearing that the rotor will frequent, usually in the center of the range of motion, like due North. Similarly place the elevation Z pulse at a bearing that is conveniently measured, like 45 or 90 degrees.

## Heading Calibration Using Sun or Moon Position

The azimuth and elevation can be calibrated to the current sun or moon position using the \XS and \XM commands, if the sun or moon is visible.  This feature is intended to be used by manually rotating an antenna towards the sun or moon and peaking for maximum solar noise or EME signals, and then executing the appropriate command.
The rotator controller clock must be accurately set to Zulu time for this feature to work accurately.

## Heading Sampling / Averaging

There are several settings to help you tweak the behavior of the heading sample.

`#define AZIMUTH_SMOOTHING_FACTOR 0`

`#define ELEVATION_SMOOTHING_FACTOR 0`

The smoothing factor settings make the unit average a fraction of the newly sampled heading with the current heading.  These factors can be set from 0 to 99.9.  The higher the number, the higher percentage of the current heading is used in the averaging formula.

`#define AZIMUTH_MEASUREMENT_FREQUENCY_MS 100`
`#define ELEVATION_MEASUREMENT_FREQUENCY_MS 100`

The measurement frequency settings determine how often headings are sampled.  The unit is in milliseconds (mS).