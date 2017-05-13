# Operation

In order to support sun and moon tracking, a time of day clock function is provided.  This uses the internal Arduino millis() function.

The clock can be queried using the \C command.  The clock can be set with the \O command like so:

    \O201401021435

The example above sets the clock to 2014-01-02 14:35 Z.  If a realtime clock (RTC) module is connected, the \O will also program the module time.

If you are using a local timezone offset as described below, if setting the clock using the \O command, you must enter the UTC (Zulu) time, not the local timezone time.

The Arduino clock frequency can be rather inaccurate over time, often losing or gaining tens of seconds a day, and it can vary with temperature.  A realtime clock module or GPS synchronization is recommended if accurate timekeeping is desired.

The internal clock does not continue to run when the Arduino loses power and must be set each session with the \O command, if an RTC or GPS is not used.

If the unit is equipped with both an RTC and GPS, the clock will synchronize off of the GPS first, and then synchronize from the RTC if GPS is not available.

If a master/slave system is used, the GPS (and RTC) can be remotely located and connected to the slave unit, and the master unit can be configured to synchronize its clock from the remote slave’s clock.

# Configuration

The clock feature is enabled with the follow line:

    #define FEATURE_CLOCK

The timekeeping accuracy of the clock can be adjusted using this setting:

    #define INTERNAL_CLOCK_CORRECTION 0

A positive number compensates for a slow clock and a negative number compensates for a fast clock.  A number of 0.00145 would make the clock run 0.145% faster.

# Timezones

The clock normally runs in UTC (Zulu) time.  If you would rather display time for a certain timezone, you can use the \V command to set the timezone offset in hours.  The command format is:

    \V[-]x[x].[x][x][x]

For example, to set a negative four hour offset from UTC:

    \V-4

To set a five and a half hour positive offset:

    \V5.5
