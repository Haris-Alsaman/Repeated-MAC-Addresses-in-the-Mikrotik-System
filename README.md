# duplicate-MAC-Address-Mikrotik


## This is the code that can be used to solve the problem of duplicated MAC addresses in the Mikrotik system.

## This code is used to solve the problem of duplicated MAC addresses in Mikrotik system. The code includes several steps, which are:

1- Put in the hostpot open user profile using the following command:


/import RepeatedMacAddresses;


2- In the same user profile, add the following command to the on-logout event:

:local z $user
/ip dhcp-server lease remove [find comment=$z];


3- In a new terminal, use the following command to create a new scheduler:



/system scheduler
add comment=FB.com/alharth6 name=reboot_MAC on-event="{\r\
    \n:foreach h1 in=[/ip dhcp-server lease find] do={\r\
    \n:local n [/ip dhcp-server lease get \$h1 comment];\r\
    \n:local ss [:len \$n];\r\
    \n:if (\"\$ss\"!=\"0\") do={/ip dhcp-server lease remove [find where comme\
    nt=\$n];}}\r\
    \n}" policy=ftp,reboot,read,write,policy,test,password,sniff,sensitive \
    start-time=startup




4- Finally, download the  file(RepeatedMacAddresses) and upload it to the file :





##FEATURES

This file is used to perform the following steps:
Check the MAC address of any device trying to connect to the network.
If a duplicate MAC address is detected, remove the current DHCP settings for this address and change them to static settings.
Delete all cookies associated with the device with the duplicate MAC address.
