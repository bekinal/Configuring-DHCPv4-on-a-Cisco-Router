<h1>Configuring DHCPv4 on a Cisco Router</h1>

<h2>Description</h2>
Project consists of configuring DHCP services on a router to dynamically assign IPv4 addresses to every endpoint and network device on each of the three networks defined.
<br />


<h2>Utilities Used</h2>

- <b>VirtualBox</b> 
- <b>Cisco Packet Tracer</b>

<h2>Environments Used </h2>

- <b>Windows 10</b>

<h2>DHCP review:</h2>
The main purpose of DHCP is to allocate IP addresses across a network on system startup. DHCP ensures that the correct configuration is entered, as client configuration is updated automatically.<br/>
DHCP servers have a User Datagram Protocol (UDP) port number of 67.<br/>
The DHCP DORA process is labeled as:<br />

- <b>Discovery:</b> The client broadcasts a DHCPDISCOVER message
- <b>Offer:</b> DHCP replies with DHCPOFFER
- <b>Request:</b> The client broadcasts DHCPREQUEST
- <b>ACK:</b> The server broadcasts a DHCPACK message (acknowledgement)
<h2>Configure DHCPv4 on R1:</h2>
Network Topology:<br/>
<img src="https://imagizer.imageshack.com/img923/2949/kDi61I.png" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
The current configuration is first saved into NVRAM on R1 and R2:<br/>
<img src="https://imagizer.imageshack.com/img923/6403/kX2PPF.png" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Global configuration mode is entered on R1 and the first 10 addresses of the following networks are excluded. This is to ensure that these IP addresses will not be automatically assigned to DHCP clients when the server is configured:<br/>
<img src="https://imagizer.imageshack.com/img923/50/2bitPk.png" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Three DHCP pools are then created for each network. Each pool is configured with network and subnet mask addresses, a default router address, and a DNS server address:<br/>
<img src="https://imagizer.imageshack.com/img922/1008/XN6FTf.png" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
DHCP is verified to be working under the PC1 desktop. Notice that the IP address is 192.168.10.11; one address above our excluded range. This is done for all other PCs. However, PC5 will not recieve an IP before configuring the DHCP relay as noted in the next section:<br/>
<img src="https://imagizer.imageshack.com/img923/277/P4S1Gk.png" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
The ipconfig /renew command has the ability to erase the network address and ask the DHCP server to assign a new one. In this case, the address is the same as before:<br/>
<img src="https://imagizer.imageshack.com/img922/3958/5PyaEB.png"/>
<br />
<br />

<h2>Setting the switches as DHCP clients:</h2>
The CLI on switch 1 is used to configure VLAN 1 to receive an IP address dynamically from router 1. The interface is then enabled, and an ip interface brief is run to verify the changes. These steps are repeated for switches 2 and 3, however switch 3 will not receive an address before configuring the DHCP relay:<br/>
<img src="https://imagizer.imageshack.com/img924/8756/7CRpzj.png" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h2>Configuring DHCP relay:</h2>
Router 2 is configured using a DHCP relay on interface Gigabit Ethernet 0/0:<br/>
<img src="https://imagizer.imageshack.com/img922/921/egHjcN.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The settings are then verified using the show running-config command:<br/>
<img src="https://imagizer.imageshack.com/img922/9995/vT8CZc.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The DHCP binding for router 1 is shown, and all devices have a DHCP assigned IP address:<br/>
<img src="https://imagizer.imageshack.com/img924/4796/kgaKzo.png" alt="Disk Sanitization Steps"/>
<br />
<br />
The PC5 interface is opened to verify that the DHCP link is working correctly:<br/>
<img src="https://imagizer.imageshack.com/img924/1037/Rxw8rY.png" alt="Disk Sanitization Steps"/>
<br />
<br />
PC5 executes a successful ping to PC1:<br/>
<img src="https://imagizer.imageshack.com/img923/4021/GnZpPc.png" alt="Disk Sanitization Steps"/>
<br />
<br />

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
