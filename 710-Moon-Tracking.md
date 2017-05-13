# Operation

To start tracking the moon, issue the \M1 command.  To stop moon tracking issue the \M0 command, or issue the Yaesu S command, press the stop button, or issue any rotation command.

# Configuration 

To activate the moon tracking functionality, uncomment the following line before compiling:

    #ifdef FEATURE_MOON_TRACKING

The following pins are available for your convenience:

Goes high when moon tracking is active:

    #define moon_tracking_active_pin 0

Ground this pin to activate moon tracking (not for use with a button):

    #define moon_tracking_activate_line 0

Use with a normally open momentary switch to ground:

    #define moon_tracking_button 0

The following settings can be adjusted to customize for your installation:

    #define MOON_TRACKING_CHECK_INTERVAL 5000
    #define MOON_AOS_AZIMUTH_MIN 0
    #define MOON_AOS_AZIMUTH_MAX 360
    #define MOON_AOS_ELEVATION_MIN 0
    #define MOON_AOS_ELEVATION_MAX 180

