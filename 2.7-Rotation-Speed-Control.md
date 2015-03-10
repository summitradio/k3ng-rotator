The controller in its simplest configuration activates the rotate_cw and rotate_ccw pins, and in the case of an AZ/EL rotator also the rotate_up and rotate_down pins.  This is sufficient for many installations, however larger antenna arrays present some physical and engineering challenges and require variable speed control and acceleration and deacceleration to avoid damage to components.  This controller supports such needs.

## Single "Always On" PWM Output / Yaesu Control Unit Interfacing

The Yaesu X1, X2, X3, and X4 speed commands are supported through a pulse-width modulation (PWM) pin connected to the Yaesu rotator controller, pin 3.  If this functionality is not desired, simply connect a jumper between pins 3 and 6 on the Yaesu controller.  This will send +5V into the rotation speed pin and will hardwire the unit for the fastest speed.

The antenna speed voltage pin can be changed by modifying this line:

`#define azimuth_speed_voltage 10`

To disable the pin, set it to 0 (zero).  Note that PWM is supported only on a specific Arduino pins; check your documentation if you intend on using a different pin.

The PWM frequency is 490 Hz.  An RC filter using a 4.7k resistor and 10 uF cap creates a 2 Hz filter which "smooths out" the squarewave and provides a nice voltage to the rotator controller.

Note that the Easycom protocol does not have a standard means of changing rotational speed.

## Switched Multiple PWM Outputs

If you need PWM outputs on the rotate CW and CCW lines instead of just one separate speed voltage pin (such as for a homebrew rotator), PWM pins can be defined here (replace the zeros with your desired pins):

`#define rotate_cw_pwm 0`

`#define rotate_ccw_pwm 0`

Elevation PWM pins can be defined here:

`#define rotate_up_pwm 0`

`#define rotate_down_pwm 0`

As if that wasn't enough, we have more choices for you.  If you would like switched PWM that comes on when azimuthal or elevation rotation is occurring, we got you covered with these pins:

`#define rotate_cw_ccw_pwm 0`

`#define rotate_up_down_pwm 0`

As with most other pin definitions, setting them to 0 (zero) disables them.  Again, remember that not all Arduino pins support PWM and you must select PWM capable pins for the output pins above for PWM to work.

## Switched Variable Frequency Outputs

If you need variable frequency outputs, pins for this can be defined here:

`#define rotate_cw_freq 0`

`#define rotate_ccw_freq 0`

`#define rotate_up_freq 0`

`#define rotate_down_freq 0`

The minimum and maximum speed frequencies are defined here:

`#define AZ_VARIABLE_FREQ_OUTPUT_LOW 1 // Frequency in hertz of minimum speed`

`#define AZ_VARIABLE_FREQ_OUTPUT_HIGH 50 // Frequency in hertz of maximum speed`

`#define EL_VARIABLE_FREQ_OUTPUT_LOW 1 // Frequency in hertz of minimum speed`

`#define EL_VARIABLE_FREQ_OUTPUT_HIGH 50 // Frequency in hertz of maximum speed`

## Automatic Azimuth Rotation Slowdown

To enable this feature, changed the 0 (zero) in this line to a 1 (one):

`#define AZ_SLOWDOWN_DEFAULT 0`

This option will slow the rotation down when automatically rotating and the target azimuth is within 10 degrees.  This can save some wear-and-tear on your rotator, especially with larger installations.  The point at which automatic slowdown kicks in can be adjusted with this line:

`#define SLOW_DOWN_BEFORE_TARGET_AZ 10`

The unit is degrees.

## Azimuth Rotation Slow Start

To enable this feature, changed the 0 (zero) in this line to a 1 (one):

`#define AZ_SLOWSTART_DEFAULT 0`

This feature starts the rotation at a slower speed and gradually ramps it up to the currently set default speed.  The amount of time spent in slow start is configured with this setting:

`#define AZ_SLOW_START_UP_TIME 2000`

The time is in milliseconds.

## Automatic Elevation Rotation Slowdown

To enable this feature, changed the 0 (zero) in this line to a 1 (one):

`#define EL_SLOWDOWN_DEFAULT 0`

This option will slow the rotation down when automatically rotating elevation and the target elevation is within 10 degrees.  The point at which automatic slowdown kicks in can be adjusted with this line:

`#define EL_SLOW_DOWN_BEFORE_TARGET_EL 10`

The unit is degrees.

## Elevation Rotation Slow Start

To enable this feature, changed the 0 (zero) in this line to a 1 (one):

`#define EL_SLOWSTART_DEFAULT 0`

The amount of time spent in slow start is configured with this setting:

`#define EL_SLOW_START_UP_TIME 2000`

The time is in milliseconds.

## Tweaking Slow Start and Slow Down Behavior

There are various settings available for altering the operation of slow start and slow down.  The operation of them is not covered here, however if you need more information, please post on the Radio Artisan group.

`#define AZ_SLOW_START_STARTING_PWM 1 // PWM starting value for slow start`

`#define AZ_SLOW_START_STEPS 20`

`#define AZ_SLOW_DOWN_PWM_START 200 // starting PWM value for slow down`

`#define AZ_SLOW_DOWN_PWM_STOP 20 // ending PWM value for slow down`

`#define AZ_SLOW_DOWN_STEPS 20`

`#define EL_SLOW_START_STARTING_PWM 1 // PWM starting value for slow start`

`#define EL_SLOW_START_STEPS 20`

`#define EL_SLOW_DOWN_PWM_START 200 // starting PWM value for slow down`

`#define EL_SLOW_DOWN_PWM_STOP 20 // ending PWM value for slow down`

`#define EL_SLOW_DOWN_STEPS 20`

## Slow Start and Slow Down for Stepping Motors

Step motors can be intolerant of high accelerations.  If the magnetic field rotation leads or lags the mechanical position of the step motor rotor excessively the motor may freeze in position. The lines in the section above allow the designer to deal with this problem.