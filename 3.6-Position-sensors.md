Currently several types of position sensors are supported:
* Potentiometer / Analog Voltage Inputs
* Rotary Encoder
* Pulse
* ADXL345 Accelerometer
* HMC5883L digital compass
* LSM303 digital compass and accelerometer

You can mix and match azimuth and elevation sensors.  For example, you can use a potentiometer for the azimuth and an ADXL345 accelerometer for the elevation.  Aren't choices great?

## Potentiometers / Analog Voltage Inputs

Most installations will use potentiometers as these are used in all mainstream commercial rotators (including Yaesu) and is often the easiest solution to implement in homebrew rotators.  If you are using a commercial rotator and are interfacing with a rotator control unit that outputs an analog voltage for the azimuth (like the Yaesu G Series), this is the option you want to use.

Potentiometer position sensors are activated with these lines:

`#define FEATURE_AZ_POSITION_POTENTIOMETER`

`#define FEATURE_EL_POSITION_POTENTIOMETER`

The input pins for potentiometer / voltage sensors are defined here:

`#define rotator_analog_az A0`

`#define rotator_analog_el 0`

You must use an analog capable pin such as A0, A1, A2, etc.  The input expects 0 to 5 volts, with 0 volts being fully counterclockwise (CCW) and 5 volts fully clockwise (CW).  (For elevation, 0 volts equates to 0 degrees, 5 volts equals 180 degrees or any maximum elevation you choose.)  The Yaesu G series rotator controllers output this voltage.

Note that if you have an azimuth only rotator, you do not need to define anything associated with elevation, and disabling `FEATURE_ELEVATION_CONTROL` will cause all elevation related parameters and features to be ignored at compile and run time.

To activate use of the Arduino/AVR analog reference pin for any analog readings (i.e. azimuth and elevation potentiometer sensors), activate `OPTION_EXTERNAL_ANALOG_REFERENCE`.  This can be used to increase the accuracy of readings by tieing the analog reference pin to the +5 volt line.

## ADXL345 Accelerometer
The ADXL345 accelerometer can be used for elevation readings.  Two libraries are supported, the [Adafruit](https://blog.adafruit.com/2013/03/26/tutorial-adxl345-digital-accelerometer-the-adafruit-learning-system/) library and the Love Electronics library _(broken link)_.  Pick one or the other, but not both.  Either one works fine.
To use the Adafruit library, uncomment this line:

`#define FEATURE_EL_POSITION_ADXL345_USING_ADAFRUIT_LIB`

To use the Love Electronics library, uncomment this line:

`#define FEATURE_EL_POSITION_ADXL345_USING_LOVE_ELECTRON_LIB`

The ADXL345 device is interfaced with the Arduino or ATMega chip via the I2C bus.  Consult [this for more information on I2C](http://www.arduino.cc/en/Reference/Wire).

Note that the accelerometer responds by rotating the sensor about the X axis.

## Rotary Encoders
Rotary encoders can be enabled with these feature defines:

`#define FEATURE_AZ_POSITION_ROTARY_ENCODER`

`#define FEATURE_EL_POSITION_ROTARY_ENCODER`

Additionally, you need to configure the rotary encoder pins here:

`#define az_rotary_position_pin1 0`

`#define az_rotary_position_pin2 0`

`#define el_rotary_position_pin1 0`

`#define el_rotary_position_pin2 0`

Replace the zeros with your pin numbers.  There are no restrictions on the pin assignments.
The last thing you need to do is set the amount of azimuthal or elevation heading change per rotary encoder pulse:

`#define AZ_POSITION_ROTARY_ENCODER_DEG_PER_PULSE 0.5`

`#define EL_POSITION_ROTARY_ENCODER_DEG_PER_PULSE 0.5`

Note that these options related to rotary encoder position sensors are enabled by default in the code:

`#define OPTION_AZ_POSITION_ROTARY_ENCODER_HARD_LIMIT `

`#define OPTION_EL_POSITION_ROTARY_ENCODER_HARD_LIMIT `

## Pulse Inputs
Pulse inputs operate by increasing or decreasing the azimuth and/or elevation headings by a preset amount each time a pulse arrives.  To enable this, first enable the appropriate feature defines:

`#define FEATURE_AZ_POSITION_PULSE_INPUT`

`#define FEATURE_EL_POSITION_PULSE_INPUT`

Then configure the pulse input pins.  Note that these pins must be interrupt capable pins.  (Pins 2 and 3 are interrupt capable on an Arduino Uno.)

`#define az_position_pulse_pin 0`

`#define el_position_pulse_pin 0`

And then set the appropriate interrupts for the pins you configured above

`#define AZ_POSITION_PULSE_PIN_INTERRUPT 0`

`#define EL_POSITION_PULSE_PIN_INTERRUPT 0`

On an Arduino Uno pin 2 uses interrupt 0 and pin 3 uses interrupt 1.  Consult [http://arduino.cc/en/Reference/AttachInterrupt](http://arduino.cc/en/Reference/AttachInterrupt) for details on hardware and interrupts.
Last, set the amount of azimuth or elevation heading change in degrees:

`#define AZ_POSITION_PULSE_DEG_PER_PULSE 0.5`

`#define EL_POSITION_PULSE_DEG_PER_PULSE 0.5`

You may also be interested in these options.  They are activated by default in the code:

`#define OPTION_AZ_POSITION_PULSE_HARD_LIMIT // stop azimuth at lower and upper limit rather than rolling over`

`#define OPTION_EL_POSITION_PULSE_HARD_LIMIT // stop elevation at lower and upper limits rather than rolling over`

`#define OPTION_POSITION_PULSE_INPUT_PULLUPS`

## HMC5883L Digital Compass

The HMC5883L digital compass is supported using the Love Electronics library.  Enable using this feature define:

`#define FEATURE_AZ_POSITION_HMC5883L`

The sensor is connected using the I2C bus.

## Incremental Rotary Encoders


Incremental rotary shaft encoders are capable of the highest stability and accuracy, considerably better than 0.1 degree. The usual disadvantage of incremental encoders is that the position value accumulated is volatile with loss of power. K3NG software eliminates this disadvantage by maintaining the headings and recalibrating the bearing during normal rotor use.  A good affordable encoder is the Omron E6B2-CWZ6C 2000P. There are many different SE configurations available, most of which are useable if accommodation is made to the Arduino interface. 

The following text only applies to the Omron E6B2.

There are two quadrature outputs A & B and an index pulse called Z. All three outputs are open-collector NPN transistors.  The power required is a voltage between +5 and +24, the Arduino Vin voltage is a convenient source. The K3NG code provides for internal pullups which will work just fine on the bench. If the distance between the SE and the Arduino is significant discrete pullups (1K ~ 5K to 5 volts) at the Arduino should be provided. A and B are 50 % duty cycle squarewaves phased 90 degrees apart. This SE outputs 2000 A/B counts per revolution. Z is a narrow pulse that occurs once per SE revolution. Direction of rotation indication can be had by reversing the A and B SE outputs to the Arduino.
Configuration:

`#define FEATURE_AZ_POSITION_INCREMENTAL_ENCODER`

`#define FEATURE_EL_POSITION_INCREMENTAL_ENCODER`

`#define OPTION_INCREMENTAL_ENCODER_PULLUPS`

`#define az_incremental_encoder_pin_phase_a 2 // must be an interrupt capable pin`

`#define az_incremental_encoder_pin_phase_b 3 // must be an interrupt capable pin`

`#define az_incremental_encoder_pin_phase_z 4`

`#define AZ_POSITION_INCREMENTAL_ENCODER_A_PIN_INTERRUPT 0             // Uno: pin 2 = interrupt 0, pin 3 = interrupt 1`

`#define AZ_POSITION_INCREMENTAL_ENCODER_B_PIN_INTERRUPT 1             // Uno: pin 2 = interrupt 0, pin 3 = interrupt 1`

Read [http://arduino.cc/en/Reference/AttachInterrupt](http://arduino.cc/en/Reference/AttachInterrupt) for details on hardware and interrupts

`#define el_incremental_encoder_pin_phase_a 2 // must be an interrupt capable pin`

`#define el_incremental_encoder_pin_phase_b 3 // must be an interrupt capable pin`

`#define el_incremental_encoder_pin_phase_z 4`

`#define EL_POSITION_INCREMENTAL_ENCODER_A_PIN_INTERRUPT 0             // Uno: pin 2 = interrupt 0, pin 3 = interrupt 1`

`#define EL_POSITION_INCREMENTAL_ENCODER_B_PIN_INTERRUPT 1  `

`#define AZ_POSITION_INCREMENTAL_ENCODER_PULSES_PER_REV 8000.0`

`#define EL_POSITION_INCREMENTAL_ENCODER_PULSES_PER_REV 8000.0`

Debugging
{under construction}


## HH-12 / AS5045
{under construction}
Feature Activation

`#define FEATURE_AZ_POSITION_HH12_AS5045_SSI`

`#define FEATURE_EL_POSITION_HH12_AS5045_SSI`

Pin Definitions

`#define az_hh12_clock_pin 11`

`#define az_hh12_cs_pin 12`

`#define az_hh12_data_pin 13`

`#define el_hh12_clock_pin 11`

`#define el_hh12_cs_pin 12`

`#define el_hh12_data_pin 13`

Hardware Connection

## LSM303
{under construction}

`#define FEATURE_AZ_POSITION_LSM303`

`#define FEATURE_EL_POSITION_LSM303 `

## Memsic 2125
Feature Activation

`#define FEATURE_EL_POSITION_MEMSIC_2125`

Pin Definitions

`#define pin_memsic_2125_x 0`

`#define pin_memsic_2125_y 0`
