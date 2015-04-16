## Preset Controls

A preset control lets the user dial a desired azimuth or elevation and initiate rotation.  Two types of preset controls are supported, potentiometers and rotary encoders.  A present start button can be defined for either.

## Preset Potentiometer

A preset potentiometer can be added by defining an analog pin in this line:

`#define az_preset_pot 0`

As of this writing the potentiometer is not on the schematic, however it's easy to connect.  Merely take a 1K to 100K potentiometer, connect one end to ground, the other end to +5 volts, and the center potentiometer wiper pin to the analog Arduino pin defined in the line above.  For good measure you can add a 0.01 uF capacitor from the +5V potentiometer to the ground pin.

The unit will automatically rotate a half second after the potentiometer is rotated.  If you would prefer a start button to initiate rotation rather than having it occur automatically, define an input pin in this line:

`#define az_preset_start_button 0`

The button is not on the schematic, but it's simply a momentary normally open button that grounds the pin upon closure.  No pull resistor is required.  Upon pressing the button, the unit will initiate rotation based on the position of the potentiometer.

Both pin settings are defaulted in the code to 0 (zero) which disables them and the preset potentiometer functionality.  (Do not enable this feature unless you have a potentiometer connected, otherwise stray noise on the analog pin will trigger false rotations.)

The settings and limits for the potentiometer can be set here:

`#define AZ_PRESET_POT_FULL_CW 0`

`#define AZ_PRESET_POT_FULL_CCW 1023`

`#define AZ_PRESET_POT_FULL_CW_MAP 180`

`#define AZ_PRESET_POT_FULL_CCW_MAP 630`

The default settings in the code are for a rotator with a starting azimuth of 180 degrees and 450 degrees of rotation capability.  A rotator with a starting point of 0 degrees and 360 degree rotation capability would be set up as so:

`#define AZ_PRESET_POT_FULL_CW 0`

`#define AZ_PRESET_POT_FULL_CCW 1023`

`#define AZ_PRESET_POT_FULL_CW_MAP 0`

`#define AZ_PRESET_POT_FULL_CCW_MAP 360`

The preset potentiometer is currently implemented only for the azimuth, not elevation.  Post on the Radio Artisan group if you're interested in an elevation preset potentiometer, or you can use the rotary encoder preset control which is implemented for both azimuth and elevation.

## Preset Rotary Encoders

Preset controls using rotary encoders are supported for both azimuth and elevation.  To enable, uncomment the appropriate lines:

`#define FEATURE_AZ_ENCODER_SUPPORT`

`#define FEATURE_EL_ENCODER_SUPPORT`

Note that FEATURE_EL_ENCODER_SUPPORT requires FEATURE_AZ_ENCODER_SUPPORT.

Pins for the controls are defined here:

`#define az_rotary_pin1 0`

`#define az_rotary_pin2 0`

`#define el_rotary_pin1 0`

`#define el_rotary_pin2 0`

The center pin of the rotary control should be grounded.  No pull up resistors on CW and CCW pins of the rotary encoder are needed as internal Arduino pullups are enabled with this line:

`#define OPTION_ENCODER_ENABLE_PULLUPS`

By default the rotary encoders have "absolute" values that are initiated with the current azimuth (and elevation) at start up.  If the azimuth or elevation is changed through other means such as commands or the manual rotation buttons, the rotary encoder presets maintain their values.  If you would like the encoder to act in a "relative" fashion, enable this line:

`#define OPTION_ENCODER_RELATIVE_CHANGE`

This will cause the rotary encoder preset controls to decrease or increase the azimuth or elevation relative to the current azimuth or elevation.  If the unit is rotating or elevating to a heading when a rotary encoder preset is invoked, the current target azimuth and/or elevation is used and adjusted.

## Speed Potentiometer

A speed potentiometer can be added by defining an analog pin in this line:

`#define speed_pot 0`

As of this writing the potentiometer is not on the schematic, however you can use a 1K to 100K potentiometer, connect one end to ground, the other end to +5 volts, and the center or wiper potentiometer pin to the analog Arduino pin defined in the line above.  You may want to add a 0.01 uF capacitor from the +5V potentiometer to the ground pin.

The setting for this pin in the code is defaulted to 0 (zero) which disables the pin.  As with all analog input pins, don't enable this feature unless you have a potentiometer connected, otherwise noise on the pin will cause false readings.

The mappings for the potentiometer can be set here:

`#define SPEED_POT_LOW 0`

`#define SPEED_POT_HIGH 1023`

`#define SPEED_POT_LOW_MAP 1`

`#define SPEED_POT_HIGH_MAP 255`

## Joystick

{under construction}

`#define FEATURE_JOYSTICK_CONTROL `

`#define pin_joystick_x A0`

`#define pin_joystick_y A1`

`#define JOYSTICK_WAIT_TIME_MS 100`
     
`//#define OPTION_JOYSTICK_REVERSE_X_AXIS`

`//#define OPTION_JOYSTICK_REVERSE_Y_AXIS`
