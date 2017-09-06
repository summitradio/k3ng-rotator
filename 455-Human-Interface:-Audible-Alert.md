# Introduction

An audible alert can be built into the using using FEATURE_AUDIBLE_ALERT.  This feature will make a pin go high or low, or emit a square wave tone.

# Settings

`#define AUDIBLE_ALERT_TYPE 1`

`#define AUDIBLE_ALERT_DURATION_MS 250`

`#define AUDIBLE_PIN_ACTIVE_STATE HIGH`

`#define AUDIBLE_PIN_INACTIVE_STATE LOW`

`#define AUDIBLE_PIN_TONE_FREQ 1000`

`#define AUDIBLE_ALERT_AT_STARTUP 1`

`#define AUDIBLE_ALERT_AT_AZ_TARGET 1`

`#define AUDIBLE_ALERT_AT_EL_TARGET 1`

### AUDIBLE_ALERT_TYPE

  1 = Logic high/low (set AUDIBLE_PIN_ACTIVE_STATE and AUDIBLE_PIN_INACTIVE_STATE)

  2 = Square Wave Tone (set AUDIBLE_PIN_TONE_FREQ to the tone frequency in hertz)

# Pins

`#define pin_audible_alert 0`

Change the 0 to the pin you want to define as your audible alert pin.