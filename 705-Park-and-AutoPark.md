# Introduction

The Park function allows you to park your antenna in a preset position quickly.  Typically this is done to protect an antenna or in the case of a mobile setup, to stow it away for travel.

# Configuration


To enable the Park functionality, uncomment this line in your features file:

    #define FEATURE_PARK

The default park azimuth and elevation is set in the settings file:

    #define PARK_AZIMUTH 360.0 * HEADING_MULTIPLIER
    #define PARK_ELEVATION 0.0 * HEADING_MULTIPLIER

Replace "360.0" with your desired park azimuth, and "0.0" with your desired park elevation.  Note that the azimuth is expressed in raw degrees, so, for example if you have a rotator with a starting azimuth point of 0 degrees and 450 degrees of rotation, you could specify 450.0 to have a parking azimuth of 90 degrees (fully counter-clockwise).

To also enable the AutoPark functionality, uncomment this line in your features file:

    #define FEATURE_AUTOPARK  

# Commands

To initiate antenna parking, execute the \P command.

The \Y command is used to query the status of AutoPark and set the AutoPark timer.

    \Y - AutoPark status
    \Yx[x][x][x] - Set AutoPark timer time (minutes) 

# Pins

Several pins are available for use with the Park and Autopark feature:

`#define button_park 0  // pull low to initiate park`

`#define park_in_progress_pin 0  // goes high when a park has been initiated and rotation is in progress`

`#define parked_pin 0            // goes high when in a parked position`

`#define pin_autopark_disable 48       // Pull low to disable autopark`

`#define pin_autopark_timer_reset 44   // Pull low to reset the autopark timer (tie in with rig PTT)`