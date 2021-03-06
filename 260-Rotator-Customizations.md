## Configuration for Other Than 450 Degree Rotators (Maximum Clockwise)

To change the rotation capability, change this setting:

`#define AZIMUTH_ROTATION_CAPABILITY_DEFAULT 450`

The settings is the rotation capability in degrees. Rotations of up to 719 degrees are supported.  Note that if Yaesu GS-232B emulation is enabled, the P36 and P45 commands will switch between 360 degree and 450 degree modes and will override this setting for the session, however when the unit is rebooted, the #define above will take effect again.  (Prior to version 1.9, the P36 and P45 commands wrote to non-volatile EEPROM.  On version 1.9 and later, they do not.)  After changing this setting you should run the \E command to re-initialize the EEPROM.

The Easycom protocol does not have a means of changing this at runtime, however the #define above is still applicable.

## Alternate Starting Points (Maximum Counterclockwise)

By default the code is configured for the azimuth rotation starting at 180 degrees or "south center" in Yaesu terminology.  The default can be changed with this setting:

`#define AZIMUTH_STARTING_POINT_DEFAULT 180`

To default to "north center" or 0 degrees, change this setting to 0.  Note that if Yaesu GS-232B emulation is enabled, the Z command will toggle between north (0 degree) and south (180 degree) center modes and will override the setting.  After changing this setting you should run the \E command to re-initialize the EEPROM.

The Easycom protocol does not have a means of changing this at runtime, however the #define above is still applicable.

## Support for Elevation Rotators That Don't Rotate (Elevate) 180 Degrees

Change this setting to alter the maximum elevation:

`#define ELEVATION_MAXIMUM_DEGREES 180`

After changing this setting you should run the \E command to re-initialize the EEPROM.
