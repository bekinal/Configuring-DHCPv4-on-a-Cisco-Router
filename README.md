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

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
