## Yaesu GS-232 Emulation and Ham Radio Deluxe

Uncomment the following lines to make the interface in Yaesu mode play better with HRD:

`#define OPTION_C_COMMAND_SENDS_AZ_AND_EL`

`#define OPTION_DELAY_C_CMD_OUTPUT`

_Note: At the time of this writing, "Yaesu GS-232B Az/El" mode in the free version HRD Rotator program has a bug in which it will not properly parse and display the elevation.  Use "Yaesu GS-232A Az/El" mode instead._

## Yaesu GS-232B Emulation

When activating `FEATURE_YAESU_EMULATION` the code defaults to GS-232A emulation, however also activating `OPTION_GS_232B_EMULATION` will default the interface protocol to GS-232B emulation.  This emulation adds support for the following commands:

* Z - toggle north and south center mode

* P36 - switch to 360 degree mode

* P45 - switch to 450 degree mode

Additionally, the output of the B, C, and C2 commands is slightly different than in GS-232A emulation.

## Yaesu Timed Buffer Commands

To enable Yaesu timed buffer commands, uncomment this line:
`#define FEATURE_TIMED_BUFFER`
Disabling this feature will free up some memory for other features.

## Easycom Protocol

Surprisingly, the Easycom protocol does not offer a means of querying the azimuth or elevation from a controller.  However, the code contains two non-standard extensions to the protocol that can be activated with these lines:

`#define OPTION_EASYCOM_AZ_QUERY_COMMAND`

`#define OPTION_EASYCOM_EL_QUERY_COMMAND`

With these options, the AZ and EL commands with no parameters will return the current azimuth or elevation.

## Tenth of a Degree Resolution

Higher precision headings are activated with this line:

`#define FEATURE_ONE_DECIMAL_PLACE_HEADINGS`

The Easycom protocol natively supports tenth of a degree resolution (i.e. 123.4 degrees), however the Yaesu protocol does not.  If this feature is enabled, the Yaesu protocol emulation will still report azimuths and elevations as integers.  With this feature enabled, the LCD display will show headings with the increased resolution.