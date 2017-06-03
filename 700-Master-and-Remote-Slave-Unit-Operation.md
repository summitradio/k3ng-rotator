# Introduction

I2C sensors offer some real neat options for sensing azimuth and elevation.  These devices are commonly used in game controllers and mobile devices to sense position or movement of the device.  Magnetometers or digital compasses measure azimuth and accelerometers can be used to sense the Earth's gravity and provide an elevation reading.
One issue facing the builder using these devices is the distance limitations of the I2C bus.  I don't know the exact limit, but anecdotal evidence leads me to believe it is several meters, which poses a problem when attempting to use these devices on an antenna up a tower or in an array perhaps several hundred meters from the operating position.
But, never fear, others have thought of this issue and as usual we have a solution.  The controller code allows you to compile code for a remote unit which interfaces with a host unit located inside.  The remote unit interfaces with the position sensor devices locally at the rotator/antenna location.  Any normally supported position sensor can be used with the remote unit, including potentiometers, rotary encoders, and I2C devices.  The host unit talks to the remote via serial or Ethernet using a simple protocol, querying it periodically for azimuth and elevation.  The control protocol also offers some ancillary commands for controlling output pins, sniffing remote serial ports, and sending data out remote serial ports which may be useful for automatting other things out at the tower such as antenna switching.  But I digress.

# Hardware

## Serial

For a serial link, the host unit needs to have two hardware serial ports, the usual Serial port ("Serial0") and Serial1.  This means that an Arduino Mega or a homebrew "bare chip" ATMega2560 or ATMega1284P is required to provide the second serial port.  The host unit Serial1 port interfaces to the Serial port (Serial0) on the remote unit.  Since the remote unit needs only one serial port, an Uno, bare chip ATMega328 or just about any Arduino variant will work.

## Ethernet

For an Ethernet master/slave you need to have two Ethernet shields, one for the master and one for the slave.  I would recommend using Arduino Mega boards or equivalent homebrew AVR units as you will need more memory to compile and run the Ethernet code.

# Serial Control Link Details

To interface the host with the remote, you simply need to connect TX on the host to RX on the remote, and RX on the host to TX on the remote.  On an Arduino Mega the Serial1 port TX and RX is pins 18 and 19, respectively.  On the remote, using an Arduino Uno, the Serial TX and RX pins are pins 1 and 0, respectively.
Depending on your particular installation, some line and signal conditioning may be required.  I have successfully sent the 9600 baud serial link though 700 meters of unshielded twisted pair CAT 5 cable, using two twisted pairs with one conductor in each pair carrying ground and the other conductor carrying the signal.  An additional conductor in the cable can carry DC voltage to power the remote unit.

A more robust solution would be to use specialized chips or a simple transistor interface to convert the 5 volt logic levels to standard RS-232 voltage levels which are +12 to 25 volts for a logic low, and -12 to -25 volts for a logic low.  This however may be overkill.

RF bypassing is a consideration as the remote will be operating in a high RF level environment and any long cabling will undoubtedly pick up RF along the way.  Bypass capacitors of 0.01 uF or 0.001 uF should be placed on both serial lines at the host and remote units.  RF shielding is another consideration for the remote unit.
The speed of the host/remote serial link is defaulted to 9600 baud, however higher speeds are possible and conversely if issues are encountered the link speed may be lowered.  Configuration tweaking details are below.
Host Unit Compilation and Configuration

The host unit needs to have the following configured:

A one computer interface protocol, such FEATURE_YAESU_EMULATION or 'FEATURE_EASYCOM_EMULATION'.
The appropriate azimuth and/or elevation position sensors pointed to the remote unit by activating FEATURE_AZ_POSITION_GET_FROM_REMOTE_UNIT and/or FEATURE_EL_POSITION_GET_FROM_REMOTE_UNIT.  Do not configure any position sensors unless they are directly connected to the host unit.  (You can have one position sensor on a remote unit and one on the host.)
For a serial link uncomment #define FEATURE_MASTER_WITH_SERIAL_SLAVE .  For an Ethernet link, uncomment #define FEATURE_MASTER_WITH_ETHERNET_SLAVE  and #define FEATURE_ETHERNET. 
Configure the usual button pins, rotate pins, etc.
For an Ethernet link, configure the Ethernet port settings:

    #define ETHERNET_MAC_ADDRESS 0xDE,0xAD,0xBE,0xEF,0xFE,0xED
    #define ETHERNET_IP_ADDRESS 192,168,1,172
    #define ETHERNET_IP_GATEWAY 192,168,1,1
    #define ETHERNET_IP_SUBNET_MASK 255,255,255,0

 … and configure the address of the remote slave:

    #define ETHERNET_SLAVE_IP_ADDRESS 192,168,1,173

#Remote Unit Compilation and Configuration

To configure a remote unit, do the following:

* Activate FEATURE_REMOTE_UNIT_SLAVE

* If using an Etherlink, activate FEATURE_ETHERNET

* Activate the appropriate azimuth and/or elevation sensors (potentiometers, rotary encoders, I2C sensors) and configure the appropriate pins.

DO NOT activate any computer interface protocols such as FEATURE_YAESU_EMULATION or FEATURE_EASYCOM_EMULATION.  The serial port on the remote will talk the host/remote protocol.

If using an Ethernet link, configure the Ethernet port on the slave unit:

    #define ETHERNET_MAC_ADDRESS 0xDE,0xAD,0xBE,0xEF,0xFE,0xEE 
    #define ETHERNET_IP_ADDRESS 192,168,1,173
    #define ETHERNET_IP_GATEWAY 192,168,1,1
    #define ETHERNET_IP_SUBNET_MASK 255,255,255,0

If using an Ethernetlink master/slave link, don’t forget to use different IP and MAC addresses for the master and slave units!

# Master/Slave Protocol

In order to operate a master/slave system you do not need to know the master/slave serial protocol, but the master/slave protocol is simple and easy to understand.  The design goals included fixed length arguments, consistent responses and event messages, and human-creatable and readable commands to insure easy testing and debugging.  Below is a summary of the protocol.

### Host to Remote Commands

    PG - ping; the remote should respond with "PG"
    AZ - read azimuth
    EL - read elevation
    DOxx - digital pin initialize as output; xx = pin # (01, 02, A0,etc.)
    DIxx - digital pin initialize as input; xx = pin #
    DPxx - digital pin initialize as input with pullup; xx = pin #
    DRxx - digital pin read; xx = pin #
    DLxx - digital pin write low; xx = pin #
    DHxx - digital pin write high; xx = pin #
    DTxxyyyy - digital pin tone output; xx = pin #, yyyy = frequency
    NTxx - no tone; xx = pin #
    ARxx - analog pin read; xx = pin #
    AWxxyyy - analog pin write; xx = pin #, yyy = value to write (0 - 255)
    SWxy - serial write byte; x = serial port # (0, 1, 2, 3), y = byte to write
    SDx - deactivate serial read event; x = port #
    SSxyyyyyy... - serial write sting; x = port #, yyyy = string of characters to send (variable length)
    SAx - activate serial read event; x = port #
    RB - reboot
    CL - read the clock

###Remote to Host Responses

    ERxx - report an error; xx = error #
    EV - report an event
    OK - report success
    CS - report a cold start

### Error Codes

    ER01 - Serial port buffer timeout
    ER02 - Command syntax error

### Events

    EVSxy - Serial port read event; x = serial port number, y = byte returned (serial port #0 = control port, port#1 = remote unit control port)

Each command and response is terminated with a carriage return.  Line feed characters may be sent either way, but are ignored.

The RB (reboot) command works on the Arduino Uno, however it locks up the Arduino Mega.

For a real world example of master and remote slave operation, check out the Frankenrotator project page.

# Serial Link Testing and Debugging

To test the remote unit, configure the code as described above, upload it to the remote unit Arduino/AVR chip and connect it to the computer with the appropriate baud rate (9600 baud by default).  Set the terminal program for carriage return and line feed.

Upon start up, the remote should send a cold start notification such as:

    CS2013042101

This indicates the version of software running on the remote.

Next, test if the remote will respond to commands.  Send a ping command:

    PG

The remote unit should respond back with a ping:

    PG

If that works, you can then read the azimuth and/or elevation from the connected sensors using the AZ and EL commands.  For fun you can play around reading and writing to pins.  The following commands turn the LED on pin 13 on and off:

    DO13
    DH13
    DL13

If you have remote unit hardware that supports additional serial interfaces like Serial1, Serial2, etc., you can read and write byte and strings on those ports.  The commands below turn on monitoring of Serial1 and sends characters out it.

    SA1
    SS1test 1 2 3

The remote unit code supports the \d (backslash d) debugging commands which activates the periodic debug dump.
If the remote unit appears to be functioning properly, it's time to connect the host and remote units, as described above.  I recommend you do this on the bench and not with the remote installed already outside.  I would also recommend doing a direct connection at +5V logic levels and forgo any line signal level converters until later after you have the units talking on the bench.

If all goes well, the host unit should be reading the azimuth and/or elevation from the remote unit and report normally, just as though the position sensors were connected directly to the host unit.  If not, the \d command should be used to view debugging information.  In host mode, the debug dump displays an additional line showing link command counters:

    debug: 2013042001BETA GS-232B
     AZ: IDLE Q: - AZ: 178.3 (raw: 178.3) Target: 0.0 (raw: 0.0) AZ Speed Norm: 255 Current: 255
     EL: IDLE Q: - EL: -50.7 Target: 0.0
     AZ: 180-450 AZ ana: 4-1009 EL ana: 2-1018
     Remote: Command: 1 Good: 31736 Bad: 0 Index: 0 CmdTouts: 0 BuffTouts: 0 Result: -50.70

Here's a description of the counters:

Command: The current or most recently executed link command.  1 = AZ, 2 = EL

Good: The number of successfully executed commands.  This counter rolls over at 65,536.

Bad: The number of unsuccessful commands.  This may included commands that timed out waiting for a response or responses received that were malformed or invalid.  This counter rolls over at 65,536.

Index: The number of bytes currently in the serial receive buffer.  A non-zero value indicates a response is in progress or errant bytes are sitting in the buffer.  (If bytes sit in the buffer for a period of time, the buffer is cleared and a buffer timeout is registered.)

CmdTouts: The number of commands that timed out awaiting a response from the remote.

BuffTouts: The number of times we received bytes from the remote, but no terminating carriage return.  Without a carriage return, the response is considered incomplete and the receive buffer on the host is cleared.

Result: This is the last valid result received from an AZ or EL command.  Normally this value will match the azimuth or elevation displayed in the debug dump lines.

A number of remote communications debugging commands are available on the host for troubleshooting and overall playing around:

    \T - sniff the remote port transmit
    \R - sniff the remote port receive
    \Z - suspend automatic remote commands
    \S - send a text string to the remote

With the \T command you can see the commands that are being transmitted to the remote.  The \R command lets you see what is coming back from the remote.  The \Z command suspends automatic commands.  This is useful if you want to temporarily stop all the AZ and EL commands spewing on the screen and want to issue some specific commands for testing purposes.  The \S command sends a text string to the remote.  The \S command in combination with the remote port receive sniffing activated (\R) basically gives you an open command prompt to the remote unit.  For example, you could do this:

    \R
    \Z
    \SPG

These commands turn on remote receive sniffing, suspend automatic commands, send a PG (ping) to the remote.  You should see a ping back.  As you would expect, with the \S command you can send all of the other host/remote protocol commands like AZ, EL, DH, DDL, etc.

Another trick you can do is the get the remote unit to do a period debug dump using this sequence:

    \Z
    \R
    \S\D

#Tweaking the Serial Link Parameters

The serial control link is configured by default for 9600 baud.  To change the link speed on the remote modify this line:

    #define CONTROL_PORT_BAUD_RATE 9600

And on the host unit, modify this line:

    #define REMOTE_UNIT_PORT_BAUD_RATE 9600

Various other host/remote communications settings:

    #define REMOTE_BUFFER_TIMEOUT_MS 250
    #define REMOTE_UNIT_COMMAND_TIMEOUT_MS 2000
    #define AZ_REMOTE_UNIT_QUERY_TIME_MS 150
    #define EL_REMOTE_UNIT_QUERY_TIME_MS 150

# Ethernet 

## Link Operation

{under construction} 

##Troubleshooting, Debugging, and Testing

{under construction}

## Tweaking and Advanced Configuration

{under construction}

    #define ETHERNET_SLAVE_RECONNECT_TIME_MS 250
    #define ETHERNET_SLAVE_TCP_PORT 23
    #define ETHERNET_PREAMBLE "K3NG" 

# Special Configurations and Features

## One Sensor on Remote Slave and One on Master Unit

The master / remote functionality can be used with one sensor connected to the master and the other connected to the remote.  On the master, specify 

    FEATURE_AZ_POSITION_GET_FROM_REMOTE_UNIT
or 

    FEATURE_EL_POSITION_GET_FROM_REMOTE_UNIT 

for whichever sensor is located on the remote unit, then specify the appropriate locally connected sensor feature for the sensor connected to the master.  The master unit will query the remote only for the _GET_FROM_REMOTE_UNIT feature you’ve configured.

## Remote Unit Pin Control and Reading

I/O pins on the remote slave can be controlled and read by the master unit for most functions.  To redirect a master unit pin function to the remote, simply add 100 to the pin number in the rotator_pins.h file of the master unit.  For example, to redirect the pin for rotate_cw to pin 13 on the remote, specify this in the rotator_pins.h file:

    #define rotate_cw 113

This will make pin 13 on the remote slave become the rotate_cw pin.

To use an analog pin in this way, do this:

    #define rotate_cw A0+100
