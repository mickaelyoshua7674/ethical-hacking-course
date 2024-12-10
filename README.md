# ethical-hacking-course
In the virtual machine configurations, the Network Adapter NAT (Network Adapter Translation) makes the virtual machine go through an abstraction of network,
making the host machine work as a router and then the VMs think that they are connected to an ethernet network (is a Virtual Network).<br>

User to Kali Linux VM:
* Login: root
* Password: toor

[Linux Commands](https://www.mediacollege.com/linux/command/linux-command.html)<br>
[Explain Linux Commands](https://explainshell.com/)

## Network Hacking
Command 'ifconfig' will show all the network interfaces connected to the computer, devices that allow to connect to a network.

### Network Basics
MAC Address (Midia Access Control) is a permanent, physical and unique address assigned to network interfaces.<br>
Whether is a wireless card, ethernet card, each card has a unique address to this card.<br>
IP Address is used on the internet to identify devices, the MAC Address is used inside a network to identify devices and transfer data between devices.

In Linux the ether showed after run the 'ifconfig' command is the MAC Address. To change it, firts desable the device by running 'ifconfig [device name] down', 
then run 'ifconfig [device name] hw (hardware) ether (the MAC Address) [the new MAC Address] (address must start with 00)'. Finally enable the changed device with 
'ifconfig [device name] up'.<br>
The MAC Address will reverse back when the computer is restarted because this changes the address in memory, not in the device itself.<br>

Wireless devices have different modes:
* Managed: will only capture packages that are destined to the MAC Address of its own (default mode)
* Monitor: will capture all packages in the network