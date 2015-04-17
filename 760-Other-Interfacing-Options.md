#Rotation Indicator Output Pin

This output pin will change state based on the rotation status.  The pin is defined on this line:

    #define rotation_indication_pin 0

Related settings:

    #define ROTATION_INDICATOR_PIN_ACTIVE_STATE HIGH
    #define ROTATION_INDICATOR_PIN_INACTIVE_STATE LOW
    #define ROTATION_INDICATOR_PIN_TIME_DELAY_SECONDS 0
    #define ROTATION_INDICATOR_PIN_TIME_DELAY_MINUTES 0

#Heading Reading Inhibit Pin

This input pin will stop azimuth and elevation readings from being taken when the pin is taken high.  The pin is defined here:

    #define heading_reading_inhibit_pin 0

This feature is useful for when sensors are interfered with during transmit.  If the transmitter PTT line is interfaced with this pin, the rotator controller will stop taking sensor measurements and will use the last headings until the heading reading inhibit pin goes low.

#Ancillary Pin Control

This feature allows the user to manually control hardware pins via the command line.

Feature Activation:

    FEATURE_ANCILLARY_PIN_CONTROL     

Command Line Commands:

    \Fxx - Turn pin off; xx = pin number
    \Nxx - Turn pin on; xx = pin number
    \Wxxyyyy - Turn on pin PWM; xx = pin number, yyy = PWM value (0-255)

#Power Switch

The controller software can control an external circuit to deactivate power to the unit after a period of inactivity.

Feature Activation:

    FEATURE_POWER_SWITCH

Pins:
    
    #define power_switch 0

Related settings:
  
    #define POWER_SWITCH_IDLE_TIMEOUT 15

The timeout unit is minutes.

#Analog Heading Output Pins

This feature will activate pins that will output voltage directly proportional to the azimuth and elevation.

Feature Activation:

    FEATURE_ANALOG_OUTPUT_PINS

Pins:

    #define pin_analog_az_out 0
    #define pin_analog_el_out 0

Related settings:

    #define ANALOG_OUTPUT_MAX_EL_DEGREES 180


