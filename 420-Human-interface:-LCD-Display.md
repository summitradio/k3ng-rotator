## LCD

A variety of LCD displays are supported and the information displayed can be customized.

## Defining LCD Characteristics 

A 20 column LCD display is preferred, but a 16 column unit can be used.  Set the number of columns and rows of your display in these lines:

`#define LCD_COLUMNS 20`

`#define LCD_ROWS 4`

The update frequency of the display can be adjusted with this setting:

`#define LCD_UPDATE_TIME 1000`

Various I2C displays use this setting:

`#define I2C_LCD_COLOR GREEN`

## Standard 4 Bit LCD Interface

To use a common classic 4 bit LCD display unit, uncomment out this line (remove the double-slashes "//") to enable it:

`#define FEATURE_4_BIT_LCD_DISPLAY`


## Adafruit I2C LCD

To use an Adafruit I2C LCD unit, uncomment this line:

`#define FEATURE_ADAFRUIT_I2C_LCD`

The I2C are hard coded for whatever Arduino board you are using and are not set in the code.  On an Uno, the I2C pins are A4 and A5.

## Yourduino LCD Display

To use the YourDuino.com I2C display, enable the feature by uncommenting: 
`#define FEATURE_YOURDUINO_I2C_LCD`

Configure the pins in the rotator_pins.h file:

`#ifdef FEATURE_YOURDUINO_I2C_LCD`

`#define En_pin  2`

`#define Rw_pin  1`

`#define Rs_pin  0`

`#define D4_pin  4`

`#define D5_pin  5`

`#define D6_pin  6`

`#define D7_pin  7`

`#endif //FEATURE_YOURDUINO_I2C_LCD`

## DFRobot LCD Display
To use a DFRobot LCD display, uncomment this line:

`#define FEATURE_RFROBOT_I2C_DISPLAY`

Settings can be customized in the rotator_settings.h file:

`#ifdef FEATURE_RFROBOT_I2C_DISPLAY`

`LiquidCrystal_I2C lcd(0x27,16,2); `

`#endif //FEATURE_RFROBOT_I2C_DISPLAY`

## LCD Customization
The LCD display can be customized with the activation of various “widgets”.  The first row of the LCD, herein reffered to as “row 1”, is reserved for status messages when an event such as rotation is in progress, but row 1 can also accommodate some widgets.

Widgets are activated by uncommenting  various features.  Each widget has customization settings in rotator_settings. h that may change the alignment and/or the row on which it appears.  Here are the widgets available:

**OPTION_DISPLAY_HHMM_CLOCK**

_Format:_ HH:MM clock on row 1

_Alignment Configuration:_ LCD_HHMM_CLOCK_POSITION (LEFT or RIGHT)

**OPTION_DISPLAY_HHMMSS_CLOCK**

_Format:_ HH:MM:SS clock on row 1

_Alignment Configuration:_ LCD_HHMMSS_CLOCK_POSITION (LEFT or RIGHT)

**OPTION_DISPLAY_ALT_HHMM_CLOCK_AND_MAIDENHEAD**

_Format:_ Alternating HH:MM Clock and Maidenhead

_Row:_ LCD_ALT_HHMM_CLOCK_AND_MAIDENHEAD_ROW

_Alignment:_ LCD_ALT_HHMM_CLOCK_AND_MAIDENHEAD_POSITION

**OPTION_DISPLAY_CONSTANT_HHMMSS_CLOCK_AND_MAIDENHEAD**

_Format:_ Continual HH:MM:SS Clock and Maidenhead

_Row:_ LCD_ALT_HHMMSS_CLOCK_AND_MAIDENHEAD_ROW

_Alignment:_ LCD_ALT_HHMMSS_CLOCK_AND_MAIDENHEAD_POSITION

**OPTION_DISPLAY_BIG_CLOCK**

_Format:_ YYYY-MM-DD HH:MM:SSZ

_Row:_ LCD_BIG_CLOCK_ROW

_Alignment:_ Always centered


**OPTION_DISPLAY_GPS_INDICATOR**

_Format:_ “GPS” when GPS tracking is active

_Row:_ LCD_GPS_INDICATOR_ROW

_Alignment:_ LCD_GPS_INDICATOR_POSITION


**OPTION_DISPLAY_MOON_TRACKING_CONTINUOUSLY**

_Format:_ Current moon azimuth and elevation

_Row:_ LCD_MOON_TRACKING_ROW

_Alignment:_ Always centered


**OPTION_DISPLAY_DIRECTION_STATUS**

_Format:_ Displays current direction (N, S, E, W, etc.)

_Row:_ Always Row 1

_Alignment:_ Always centered


**OPTION_DISPLAY_SUN_TRACKING_CONTINUOUSLY**

_Format:_ Current sun azimuth and elevation

_Row:_ LCD_SUN_TRACKING_ROW

_Alignment:_ Always centered

**OPTION_DISPLAY_MOON_OR_SUN_TRACKING_CONDITIONAL**

_Format:_ Displays sun or moon tracking when it is activate.  A “*” appears on each side during AOS and a “-” appears on each side during LOS.

_Row:_ LCD_MOON_OR_SUN_TRACKING_CONDITIONAL_ROW

_Alignment:_ Always centered

_Customization:_

`#define TRACKING_ACTIVE_CHAR "*"`

`#define TRACKING_INACTIVE_CHAR "-"`

**OPTION_CLOCK_ALWAYS_HAVE_HOUR_LEADING_ZERO**

This option activates the hour leading zero on several of the different clock widgets.  For example, 1:23 will be display as 01:23.

