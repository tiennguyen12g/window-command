# window-command
#### Manage Ip and connection.
1. Change name when out internet device connect (phone, dcom ...)
1.1 Check the list interface in pc
```
   netsh interface show interface

--output:
C:\Users\tienn>netsh interface show interface

Admin State    State          Type             Interface Name
-------------------------------------------------------------------------
Enabled        Disconnected   Dedicated        VPN - VPN Client
Enabled        Disconnected   Dedicated        Local Area Connection
Enabled        Disconnected   Dedicated        Local Area Connection 2
Enabled        Connected      Dedicated        Ethernet 2
Enabled        Disconnected   Dedicated        HotspotShield Network Adapter
Enabled        Connected      Dedicated        Ethernet
Enabled        Connected      Dedicated        Ethernet 6
```
1.2 Change the name of the device internet.
```
netsh interface set interface name="Old Name" newname="New Name"

--run again to get new update: netsh interface show interface
```

