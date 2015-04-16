#Operation

DS1307 and PCF8583 realtime (RTC) clock modules are supported.  These modules maintain the time, even when not powered as they have self-contained batteries.

The time of the realtime clock is set by the \O command, described above in the section on the Clock functionality.  If the rotator controller is also GPS equipped, the RTC will be periodically updated with the GPS time.

Note that cheap RTC modules may have issues with timekeeping accuracy and battery charging.  Consult Google if you have issues.

#Configuration

To enable DS1307 module support, uncomment this line:

    #define FEATURE_RTC_DS1307

To enable PCF8583 module support, uncomment this line:

    #define FEATURE_RTC_PCF8583

This setting defines how often the internal Arduino clock is synchronized with the RTC module:

    #define SYNC_WITH_RTC_SECONDS 59

This setting configures how often the RTC is synchronized with GPS, if it is available:

    #define SYNC_RTC_TO_GPS_SECONDS 12

#Hardware Connection

Both modules connect to the I2C bus, the SDA and SCA pins (pins 20 and 21 on an Arduino Mega).

#Debugging

Use the \d command to see the status of the clock.  In the example below the clock status is "RTC_SYNC".

    debug: 	1.9.2014021501-UNSTABLE		2014-02-16 01:38:06Z	RTC_SYNC	40.8806 -75.5865		GS-232B
	AZ: IDLE	Q: - AZ: 240.0 (raw: 240.0) (raw: 0.0)  Analog: 140 (4-1009) [180+450]  AZ Speed Norm: 253 Current: 253	Offset: 0.00
	EL: IDLE	Q: - EL: 24.0 EL Analog: 141 (2-1018)   EL Speed Norm: 253 Current: 253	Offset: 0.00
	moon: AZ: 103.90 EL: 21.27	TRACKING_INACTIVE 	sun: AZ: 284.64 EL: -34.65	TRACKING_INACTIVE

The clock states are:

  FREE_RUNNING - No synchronization with RTC or GPS
  RTC_SYNC - Using the realtime clock for time
  GPS_SYNC - Synchronized to GPS
  SLAVE_SYNC - The master unit clock is synchronized to the slave unit clock
  SLAVE_SYNC_GPS - The master unit clock is synchronized to the slave unit clock and the slave is synchronized to GPS
