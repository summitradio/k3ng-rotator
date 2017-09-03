## Overlap LED

To activate the Overlap LED line, change the 0 (zero) in this line to whatever pin you wish to use in [rotator_pins.h](https://github.com/k3ng/k3ng_rotator_controller/blob/master/rotator_pins.h):

`#define overlap_led 0`

To disable, set the pin to 0.  The Overlap LED will be activated whenever the azimuth is greater than the rotator 
starting (fully CCW) azimuth.

To have the LED blink, set the `OPTION_BLINK_OVERLAP_LED` feature in [rotator_features.h](https://github.com/k3ng/k3ng_rotator_controller/blob/master/rotator_features.h) .  The blink rate can be varied with the `OPTION_OVERLAP_LED_BLINK_MS` setting in [rotator_settings](https://github.com/k3ng/k3ng_rotator_controller/blob/master/rotator_settings.h).

## Rotation Indicator LED

This output pin will change state based on the rotation status.  The pin is defined on this line:

`#define rotation_indication_pin 0`

Related settings:

`#define ROTATION_INDICATOR_PIN_ACTIVE_STATE HIGH`

`#define ROTATION_INDICATOR_PIN_INACTIVE_STATE LOW`

`#define ROTATION_INDICATOR_PIN_TIME_DELAY_SECONDS 0`

`#define ROTATION_INDICATOR_PIN_TIME_DELAY_MINUTES 0`

## Park LED

This pin goes high when the rotation system has been parked.

`#define parked_pin 0  `

## Park In Progress LED

This pin will go high when there is a rotation park operation in progress.

`#define park_in_progress_pin 0 `

## Serial Activity LED

If defined this pin will go high when there is serial control port activity.

`#define serial_led 0 `

## Run LED

This pin will alternate high and low when the system is running and can be used to drive an LED.  This can be useful on headless units that lack an LCD display or serial port control, or remote slave units.

`#define blink_led 0`

## GPS Sync LED

This pin when defined will go high when GPS tracking is enabled and there is a valid satellite fix. 

`#define gps_sync 0`

## Moon Tracking LED

This pin goes high when moon tracking is activated (regardless of moon visibility).

`#define moon_tracking_active_pin 0 `

## Sun Tracking LED

This pin goes high when sun tracking is activated (regardless of sun visibility).

`#define sun_tracking_active_pin 13 `

## Heading Analog Output Pins

Two pins are available to driving analog meters for azimuth and elevation headings.  This is activated with:

`#define FEATURE_ANALOG_OUTPUT_PINS`

The pins are defined in this section of code:

`#define pin_analog_az_out 0`

`#define pin_analog_el_out 0`

Additionally, the corresponding elevation voltage maximum can be set in your settings file:

`#define ANALOG_OUTPUT_MAX_EL_DEGREES 180`

## Rotation LEDs

Additional optional pins are provided for driving LEDs to indicate rotation"

`\\#define pin_led_cw 0`

`\\#define pin_led_ccw 0`

`\\#define pin_led_up 0`

`\\#define pin_led_down 0`

Uncomment the lines and change the 0s to the pins you want to configure.

The active and inactive levels of these pins can be configured in your settings file:

`#define PIN_LED_ACTIVE_STATE HIGH`

`#define PIN_LED_INACTIVE_STATE LOW`
