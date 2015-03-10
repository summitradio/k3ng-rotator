{under construction}

## Azimuth
`#define rotate_cw 6`              // goes high to activate rotator R (CW) rotation - pin 1 on Yaesu connector

`#define rotate_ccw 7`             // goes high to activate rotator L (CCW) rotation - pin 2 on Yaesu connector

`#define rotate_cw_ccw  0`         // goes high for both CW and CCW rotation

`#define rotate_cw_pwm 0`          // optional - PWM CW output - set to 0 to disable (must be PWM capable pin)

`#define rotate_ccw_pwm 0`         // optional - PWM CCW output - set to 0 to disable (must be PWM capable pin)

`#define rotate_cw_ccw_pwm 0`      // optional - PWM on CW and CCW output - set to 0 to disable (must be PWM capable pin)

`#define rotate_cw_freq 0`         // optional - CW variable frequency output

`#define rotate_ccw_freq 0`        // optional - CCW variable frequency output

`#define az_stepper_motor_pulse 0`

`#define az_stepper_motor_direction 0`

## Elevation
`#define rotate_up 8 `              // goes high to activate rotator elevation up

`#define rotate_down 9`             // goes high to activate rotator elevation down

`#define rotate_up_or_down 0`      // goes high when elevation up or down is activated

`#define rotate_up_pwm 0`           // optional - PWM UP output - set to 0 to disable (must be PWM capable pin)

`#define rotate_down_pwm 0`         // optional - PWM DOWN output - set to 0 to disable (must be PWM capable pin)

`#define rotate_up_down_pwm 0`      // optional - PWM on both UP and DOWN (must be PWM capable pin)

`#define rotate_up_freq 0`          // optional - UP variable frequency output

`#define rotate_down_freq 0`        // optional - UP variable frequency output

`#define el_stepper_motor_pulse 0`

`#define el_stepper_motor_direction 0`

## Brake Operation

Two I/O pins can be defined for brake operation, one for azimuth and one for elevation:

`#define brake_az 0`

`#define brake_el 0`

A setting of zero (0) disables the line.

The brake engage delay time is configured with these settings:

`#define AZ_BRAKE_DELAY 3000`

`#define EL_BRAKE_DELAY 3000`

The delay time is in milliseconds.  Each brake line goes high when rotation is in progress, so the lines can be used to engage a relay which would supply voltage to activate a solenoid and disengage a brake.
## Rotation Pin Logic State Inversion

Normally the rotate_cw, rotate_ccw, rotate_up, and rotate_down pins operate in an "inactive low / active high" manner.  If you wish to invert this behavior, modify these lines, switching the LOW and HIGH values:

`#define ROTATE_PIN_INACTIVE_VALUE LOW`

`#define ROTATE_PIN_ACTIVE_VALUE HIGH`
