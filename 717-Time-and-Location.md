Both the moon and sun tracking features require the exact time and location for the tracking algorithms.  The internal clock functionality is described further below.  The location of the unit can be determined one of several ways:

1. Statically configured in the code with these settings:
    
    #define DEFAULT_LATITUDE 40.889958
    #define DEFAULT_LONGITUDE -75.585972

2. Configured at runtime using the \G command to set the Maidenhead grid square.  For example:

    \GFN20EV
  
This would set the coordinates for the center of grid square FN20ev.  Note that a six character grid square is required.

3. Use the GPS synchronization functionality, described further below.

##Tracking Status

Currently the status of moon and sun tracking can be viewed using the debug output, the \d command.