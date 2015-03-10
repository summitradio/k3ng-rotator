## Button Switch Interfacing

All button switches are momentary normally off switches.  When the button is pressed, the switch is closed which forces the Arduino interface pin to 0 volts or a logic low level.

## Manual Rotation

Buttons are provided for manual rotation control if desired.  These buttons can be omitted without any code changes, if manual button rotation control is not desired.  When not using a button, set its pin to 0 (zero) in the code prior to compilation:

`#define button_cw 0`

`#define button_ccw 0`

`#define button_up 0`

`#define button_down 0`

There is an optional stop button feature that can be enabled by assigning a pin number to this line:

`#define button_stop 0`

The stop button is mainly for halting automatic rotation initiated by the computer serial interface and not for stopping manual rotating activated by rotate CW and rotate CCW button depressing.

The `OPTION_BUTTON_RELEASE_NO_SLOWDOWN` is available to disables automatic slowdown when manual rotation buttons are depressed and released. 

## Park Function

The Park feature enables the user to press a button and have the rotator rotate to a preset azimuth (and elevation), usually to safeguard antennas from high winds or tuck away antennas on mobile arrays for travel.  The Park function is enabled by activating FEATURE_PARK and defining a pin for the button here:

`#define button_park 0`

The preset azimuth and/or elevation is set here:

`#define PARK_AZIMUTH 0.0`

`#define PARK_ELEVATION 0.0`

Park can also be initiated with the \P command using the serial control port or Ethernet interface.
Controls