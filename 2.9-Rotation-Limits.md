## Rotation Limits

Software
If you would like to set software limits for the azimuth rotation commands and buttons uncomment this line:

`#define OPTION_AZ_MANUAL_ROTATE_LIMITS`

...and customize these settings:

`#define AZ_MANUAL_ROTATE_CCW_LIMIT 185`

`#define AZ_MANUAL_ROTATE_CW_LIMIT 535`

The above settings will stop CCW rotation when an azimuth of 185 is reached, and stop CW rotation when 175 degrees is reached ("5:30" on a 180 degree starting azimuth rotator.)
This functionality is useful if for some reason you do not want your rotation system going beyond a certain point due to physical limits.

There is a corresponding feature and settings for elevation rotation limits:
`#define OPTION_EL_MANUAL_ROTATE_LIMITS`
`#define EL_MANUAL_ROTATE_DOWN_LIMIT -1`
`#define EL_MANUAL_ROTATE_UP_LIMIT 181`

## Hardware / Limit Switches
{under construction}
`#define FEATURE_LIMIT_SENSE`

`#define az_limit_sense_pin 0  // input - low stops azimuthal rotation`

`#define el_limit_sense_pin 0  // input - low stops elevation rotation`