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
2.1 Get latest vcpkg zip file from https://github.com/microsoft/vcpkg/releases (e.g. https://github.com/microsoft/vcpkg/archive/2019.09.zip) and extract it to a folder of your choice (e.g. C:\vcpkg\)
2.2 Extract file and go to ...\vcpkg\.  
2.3 Manual click to run "bootstrap-vcpkg.bat" in folder vcpkg.  
2.4 vcpkg.exe integrate install.  
2.5 vcpkg.exe install curl.  
Done.

#### 3. Set priority internet in window 10
3.1 Open PowerShell as Administrator
3.2 Check interface metric by
```
PS C:\WINDOWS\system32> Get-NetIPInterface

--output:
ifIndex InterfaceAlias                  AddressFamily NlMtu(Bytes) InterfaceMetric Dhcp     ConnectionState PolicyStore
------- --------------                  ------------- ------------ --------------- ----     --------------- -----------
50      Samsung 2A                      IPv6                  1500              25 Enabled  Connected       ActiveStore
4       Ethernet 2                      IPv6                  1500              25 Enabled  Connected       ActiveStore
15      HotspotShield Network Adapter   IPv6                  1500              25 Enabled  Disconnected    ActiveStore
10      VPN - VPN Client                IPv6                  1500              35 Enabled  Disconnected    ActiveStore
21      Local Area Connection 2         IPv6                 65535               5 Disabled Disconnected    ActiveStore
3       LAN FPT                         IPv6                  1500              35 Enabled  Connected       ActiveStore
13      Local Area Connection           IPv6                  1500              25 Disabled Disconnected    ActiveStore
1       Loopback Pseudo-Interface 1     IPv6            4294967295              75 Disabled Connected       ActiveStore
50      Samsung 2A                      IPv4                  1500              25 Enabled  Connected       ActiveStore
4       Ethernet 2                      IPv4                  1500              25 Disabled Connected       ActiveStore
15      HotspotShield Network Adapter   IPv4                  1500              10 Enabled  Disconnected    ActiveStore
10      VPN - VPN Client                IPv4                  1500               1 Enabled  Disconnected    ActiveStore
21      Local Area Connection 2         IPv4                 65535               5 Disabled Disconnected    ActiveStore
3       LAN FPT                         IPv4                  1500              35 Enabled  Connected       ActiveStore
13      Local Area Connection           IPv4                  1500              25 Enabled  Disconnected    ActiveStore
1       Loopback Pseudo-Interface 1     IPv4            4294967295              75 Disabled Connected       ActiveStore
```
3.3 Let see "LAN FPT" has interface metric number 35 and Samsung 2A has interface metric number 25.
Now if you want "LAN FPT" is priority than Samsung 2A. You have to run this:
```
Set-NetIPInterface -InterfaceAlias "LAN FPT" -InterfaceMetric 20
```
*Note: metric number much be a number divisible by five.
Done.
