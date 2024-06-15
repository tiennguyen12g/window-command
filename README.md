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
3.4 Delete an Virtual Ethernet
```
Remove-VMSwitch -Name "Primary Virtual Switch"
and check again
Get-VMSwitch
```
#### 4. List check IP, Port commands
4.1 
```
netstat -a -b
```
or
```
route print
```
(Add -n to stop it trying to resolve hostnames, which will make it a lot faster.)

Note Dane's recommendation for TCPView. It looks very useful!

-a Displays all connections and listening ports.

-b Displays the executable involved in creating each connection or listening port. In some cases well-known executables host multiple independent components, and in these cases the sequence of components involved in creating the connection or listening port is displayed. In this case the executable name is in [] at the bottom, on top is the component it called, and so forth until TCP/IP was reached. Note that this option can be time-consuming and will fail unless you have sufficient permissions.

-n Displays addresses and port numbers in numerical form.

-o Displays the owning process ID associated with each connection.

4.2 In search on Start fill it "Resource Monitor"
It will show a GUI of Network connection
4.3 Allow port in firewall on windown
Run cmd with Administrator permit
Create:
```
netsh advfirewall firewall add rule name="TCP Port 50001" dir=in action=allow protocol=TCP localport=50001
```
Check firewall port status
```
netsh advfirewall firewall show rule name="TCP Port 30000"
```
Delete:
```
netsh advfirewall firewall delete rule name="TCP Port 6624" protocol=TCP localport=6624
```

