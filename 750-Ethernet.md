#Operation

The code supports the standard Arduino Ethernet shield (http://arduino.cc/en/Main/ArduinoEthernetShield#.Uv_5G9-9uR0) and any compatible shields.  The unit accepts up to two telnet connections and all commands and protocols supported on the serial control port are supported on the Ethernet port.

The default configuration listens on two TCP ports, port 23 and port 24.  Port 23 is the standard telnet port.  You can telnet to the Ethernet port on most computer operating systems using the telnet command like so:

    telnet 192.168.1.173

To telnet to port 24, use this command:

    telnet 192.168.1.173 24

Note that only one telnet client can connect to a port at a time.  If you connect more than one client, the operation will be erratic.

#Configuration

The Ethernet functionality is enabled with this option:

    #define FEATURE_ETHERNET

The layer two MAC address of the Ethernet port is set here, in the rotator_settings.h file:

    #define ETHERNET_MAC_ADDRESS 0xDE,0xAD,0xBE,0xEF,0xFE,0xED

The layer three IP address, gateway, and subnet mask is set here:

    #define ETHERNET_IP_ADDRESS 192,168,1,173
    #define ETHERNET_IP_GATEWAY 192,168,1,1
    #define ETHERNET_IP_SUBNET_MASK 255,255,255,0

The layer four TCP ports that are the telnet listeners are configured here:

    #define ETHERNET_TCP_PORT_0 23
    #define ETHERNET_TCP_PORT_1 24

#Testing and Debugging

{under construction}
