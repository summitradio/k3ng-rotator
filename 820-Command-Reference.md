# Yaesu GS-232 Commands

    B              - Report elevation
    C              - Report azimuth
    C2             - Report azimuth and elevation
    S              - Stop all rotation
    A              - Stop azimuth rotation
    E              - Stop elevation rotation
    L              - Rotate azimuth left (CCW)
    R              - Rotate azimuth right (CW)
    D              - Rotate elevation down
    U              - Rotate elevation up
    Mxxx           - Move to azimuth
    Wxxx yyy       - Move to azimuth xxxx and elevation yyy
    X1             - Change to azimuth rotation speed setting 1
    X2             - Change to azimuth rotation speed setting 2
    X3             - Change to azimuth rotation speed setting 3
    X4             - Change to azimuth rotation speed setting 4
    O              - Azimuth offset calibration
    F              - Azimuth full scale calibration
    O2             - Elevation offset calibration
    F2             - Elevation full scale calibration
    P36            - Switch to 360 degree mode
    P45            - Switch to 450 degree mode
    Z              - Toggle north / south centered mode
    H              - Help
# Easycom Commands

    AZ             - (No Parameters) Read azimuth
    AZ [xx]x[.xxx] - Initiate azimuth rotation to a heading	
    EL             - (No Parameters) Read elevation
    EL [xx]x[.xxx] - Initiate elevation rotation to a heading
    ML             - Move Left (CCW)
    MR             - Move Right (CW)
    MU             - Move Up
    MD             - Move Down
    SA             - Stop azimuth movement
    SE             - Stop elevation rotation

# Backslash Commands

Backslash commands are available by default and are available regardless of activation of Yaesu or Easycom commands.

    \Ax[xxx][.][xxxx] - manually set azimuth
    \Ax[x][x]         - manually set azimuth (FEATURE_AZ_POSITION_ROTARY_ENCODER & FEATURE_AZ_POSITION_PULSE_INPUT)
    \Bx[xxx][.][xxxx] - manually set elevation
    \Bx[x][x]         - manually set elevation (FEATURE_EL_POSITION_ROTARY_ENCODER & FEATURE_EL_POSITION_PULSE_INPUT)
    \C                - display clock
    \D                - activate debug logs
    \E                - initialize EEPROM
    \Fxx              - change I/O pin LOW, xx = pin number
    \Gxxxxxx          - set coordinates using grid square
    \Ix[x][x]         - set az starting point
    \I                - display the current az starting point
    \Jx[x][x]         - set az rotation capability
    \J                - display the current az rotation capability
    \Kx               - force disable the az brake even if a pin is defined (x: 0 = enable, 1 = disable)
    \K                - display the current az brake state
    \L                - rotate to long path
    \Mx               - activate or deactivate moon tracking (x: 0 = deactivate, 1 = activate)
    \Nxx              - change I/O pin HIGH, xx = pin number
    \Oyyyymmddmm      - set clock
    \P                - park antenna
    \Q                - Save settings in the EEPROM and restart
    \R                - remote port receive sniff activate/deactivate
    \S[string]        - send text out remote port
    \T                - remote port transmit sniff activate/deactivate
    \Ux               - activate or deactivate sun tracking (x: 0 = deactivate, 1 = activate)
    \V[-]x[.][x][x][x]- configure clock timezone offset in hours
    \Wxxyyy           - turn on pin PWM; xx = pin number, yyy = PWM value (0-255)
    \XM               - calibrate azimuth and elevation to current moon position
    \XS               - calibrate azimuth and elevation to current sun position
    \X0               - clear calibration to defaults
    \Z                - suspend automatic remote commands

    UNDER_DEVELOPMENT_REMOTE_UNIT_COMMANDS

    \?ARxx            - analog pin read; xx = pin #
    \?AS              - query azimuth rotation status
    \?AWxxyyy         - analog pin write; xx = pin #, yyy = value to write (0 - 255)
    \?AZ              - query azimuth
    \?CL              - read clock
    \?DLxx            - digital pin write low; xx = pin #
    \?DHxx            - digital pin write high; xx = pin # 
    \?DIxx            - digital pin initialize as input; xx = pin #
    \?DOxx            - digital pin initialize as output; xx = pin # (01, 02, A0,etc.)
    \?DPxx            - digital pin initialize as input with pullup; xx = pin #
    \?DRxx            - digital pin read; xx = pin #
    \?DTxxyyyy        - digital pin tone output; xx = pin #, yyyy = frequency
    \?EL              - query elevation
    \?ES              - query elevation rotation status
    \?GAxxx.x         - go to AZ xxx.x
    \?GExxx.x         - go to EL
    \?GS              - query GPS sync status
    \?NTxx            - no tone; xx = pin #
    \?PG              - ping remote
    \?RD              - rotate down
    \?RC              - read coordinates
    \?RL              - rotate left
    \?RR              - rotate right
    \?RU              - rotate up
    \?SA              - stop azimuth rotation
    \?SE              - stop elevation rotation
    \?SS              - stop all rotation
    \!OKxx[]          - response to command sent to remote unit, valid command
    \!??xx[]          - response to command sent to remote unit, error