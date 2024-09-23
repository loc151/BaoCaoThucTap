|STT|Guidance|Compliance|Demo|
|:---|:---|:---|:---|
|01|Update the router to the latest firmware version|||
|02|Enable stateful packet inspection (SPI)|||
|03|Disable ping (ICMP) response on WAN port|||
|04|Disable UPnP (universal plug-and-play)|||
|05|Disable IDENT (port 113)|||
|06|Disable remote management of the router|||
|07|Change the default administrator password|||
|08|The settings for a firewall policy should be as specific as possible. Do not use 0.0.0.0 as an address|||
|09|Check for incoming/outgoing traffic security policy|||
|10|Check for firewall firmware / OS updates|||
|11|Allow only HTTPS access to the GUI and SSH access to the CLI|||
|12|Re-direct HTTP GUI logins to HTTPS|||
|13|Change the HTTPS and SSH admin access ports to non-standard ports|||
|14|Restrict logins from trusted hosts|||
|15|Set up two-factor authentication for administrators|||
|16|Create multiple administrator accounts|||
|17|Modify administrator account lockout duration and threshold values|||
|18|Check if all management access from the Internet is turned off, if it does not have a clear business need. At most, HTTPS and PING should be enabled|||
|19|Ensure that your SNMP settings are using SNMPv3 with encryption and configure your UTM profiles|||
|20|All firewall policies should be reviewed every 3 months to verify the business purpose|||
