Moon Tracking
Operation

To start tracking the moon, issue the \M1 command.  To stop moon tracking issue the \M0 command, or issue the Yaesu S command, press the stop button, or issue any rotation command.
Configuration 

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

Sun Tracking
Operation
To start tracking the sun, issue the \U1 command.  To stop moon tracking issue the \U0 command, or issue the Yaesu S command, press the stop button, or issue any rotation command.
Configuration
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

Time and Location
Both the moon and sun tracking features require the exact time and location for the tracking algorithms.  The internal clock functionality is described further below.  The location of the unit can be determined one of several ways:
1. Statically configured in the code with these settings:
 #define DEFAULT_LATITUDE 40.889958
 #define DEFAULT_LONGITUDE -75.585972
2. Configured at runtime using the \G command to set the Maidenhead grid square.  For example:
\GFN20EV
  This would set the coordinates for the center of grid square FN20ev.  Note that a six character grid square is required.
3. Use the GPS synchronization functionality, described further below.
Tracking Status
Currently the status of moon and sun tracking can be viewed using the debug output, the \d command.  (A future update will provide a more user-friendly display.)
