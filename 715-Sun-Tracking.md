#Operation

To start tracking the sun, issue the \U1 command.  To stop moon tracking issue the \U0 command, or issue the Yaesu S command, press the stop button, or issue any rotation command.

#Configuration

To activate the sun tracking functionality, uncomment the following line before compiling:

    #define FEATURE_SUN_TRACKING

The following pins are your friends:

Goes high when sun tracking is active:

    #define sun_tracking_active_pin 13

Ground this pin to activate sun tracking (not for use with a button):

    #define sun_tracking_activate_line 0

Use with a normally open momentary switch to ground:

    #define sun_tracking_button 30

The following settings can be adjusted to customize for your installation:

    #define SUN_TRACKING_CHECK_INTERVAL 5000
    #define SUN_AOS_AZIMUTH_MIN 0
    #define SUN_AOS_AZIMUTH_MAX 360
    #define SUN_AOS_ELEVATION_MIN 0
    #define SUN_AOS_ELEVATION_MAX 180

