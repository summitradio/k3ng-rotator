The unit is interfaced to the computer simply using the native Arduino USB port.  Currently Yaesu and Easycom protocols are supported.

To enable Yaesu GS-232A emulation, uncomment this line:

`#define FEATURE_YAESU_EMULATION`

To activate Yaesu GS-232B emulation, also uncomment this line:

`#define OPTION_GS_232B_EMULATION`

To activate Easycom emulation, uncomment just this line:

`#define FEATURE_EASYCOM_EMULATION`

Further information specific to the protocols is below.
