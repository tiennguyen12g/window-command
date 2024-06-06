# window-command
### Manage Ip and connection.
#### 1. Change name when out internet device connect (phone, dcom ...)

##### 1.1 Check the list interface in pc
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
##### 1.2 Change the name of the device internet.
```
netsh interface set interface name="Old Name" newname="New Name"

--run again to get new update: netsh interface show interface
```

#### 2. Install libcurl.lib to Visual 2022.
2.1
```
Get latest vcpkg zip file from https://github.com/microsoft/vcpkg/releases (e.g. https://github.com/microsoft/vcpkg/archive/2019.09.zip) and extract it to a folder of your choice (e.g. C:\vcpkg\)
```
2.2 Extract file and go to ...\vcpkg\
2.3 Manual click to run "bootstrap-vcpkg.bat" in folder vcpkg
2.4 vcpkg.exe integrate install
2.5 vcpkg.exe install curl
Done.

