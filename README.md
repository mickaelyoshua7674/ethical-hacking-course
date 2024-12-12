# ethical-hacking-course
In the virtual machine configurations, the Network Adapter NAT (Network Adapter Translation) makes the virtual machine go through an abstraction of network,
making the host machine work as a router and then the VMs think that they are connected to an ethernet network (is a Virtual Network).<br>

User to Kali Linux VM:
* Login: root
* Password: toor

[Linux Commands](https://www.mediacollege.com/linux/command/linux-command.html)<br>
[Explain Linux Commands](https://explainshell.com/)

## Network Hacking
Command `ifconfig` will show all the network interfaces connected to the computer, devices that allow to connect to a network.

### Network Basics
MAC Address (Midia Access Control) is a permanent, physical and unique address assigned to network interfaces.<br>
Whether is a wireless card, ethernet card, each card has a unique address to this card.<br>
IP Address is used on the internet to identify devices, the MAC Address is used inside a network to identify devices and transfer data between devices.

In Linux the ether showed after run the `ifconfig` command is the MAC Address. To change it, firts desable the device by running `ifconfig [device name] down`, 
then run `ifconfig [device name] hw (hardware) ether (the MAC Address) [the new MAC Address] (address must start with 00)`. Finally enable the changed device with 
`ifconfig [device name] up`.<br>
The MAC Address will reverse back when the computer is restarted because this changes the address in memory, not in the device itself.<br>

Wireless devices have different modes:
* Managed: will only capture packages that are destined to the MAC Address of its own (default mode)
* Monitor: will capture all packages in the network

### Packet Sniffing (Using Airodump-NG)
With the wireless adapter in Monitor mode now is possible to capture packets from the wireless neetwork without connect to it.<br>
To run the program execute `airodump-ng [device name]`. Then it will show all the wireless networks around and will display some information about then.

What will be shown:
* BSSID: MAC Address
* PWR: Network's power/strength (higher the number, better the signal)
* Beacons: Frames send by the network to broadcast its existence, even if the network is hidden, this will be send by the network
* #Data: Number of data packets sent
* #/s: Number of data packets collected in the past 10 seconds
* CH: Channel were the network works
* MB: Maximum speed supported by the network
* ENC: Encription
* CIPHER: Cipher used in the network
* AUTH: Authentication used in the network
* ESSID: Network's names

#### Wifi Bands
Define what frequency range that can be used to broadcast the signal. The 2 main frequencies used in wifi networks are 2.4GHz and 5GHz.<br>
Not all wireless adapters supports 5GHz, is necessary an adapter that supports this fequency to be able to see the network with 'Airodump-NG'.<br>
To listen to 5GHz just tell airdump-ng to do so running the command `airodump-ng --band a (band that supports 5GHz) [wireless adapter name]`.<br>
With `airodump-ng --band abg (band that supports 5GHz and 2.4GHz) [wireless adapter name]` is possible to see both frequencies at the same time. This method is slower 
because is needed more time for the wireless adapter to search all the bands. Also is needed a powerfull adapter to search all.

#### Targeted Packet Sniffing
`airodump-ng --bssid [target MAC Address] --channel [the network channel] --write [file name to store all the data collected] [wireless adapter name]`. Running this will show only one
network and also show all the devices connected to this network. The new informations are:
* BSSID: Network MAC Address
* STATION: MAC Address of the devices conneted to the network
* PWR: Power, signal strength
* Rate: Device's speed
* Lost: Amount of data loss
* Frames: Amount of frames / packets that were captured
* Probe: If the device are trying to connect to the network

The main file created from running this command is the 'test-01.cap', it will contain everything that was sent to and from the target network. The collected packets are encrypted.

#### Deauthentication Attack
Allow to disconnect any device from any network before connecting to any of these networks and without the need to know password for the network.<br>
How it works: pretend to be the client by changing the MAC Address to the same as the client and tell the router that I want to disconnect from the network. Then pretend to be the router by changing the MAC Address to the same as the router and tell the client that you requested to be disconnected so I'm going to disconnect you. There is no need to do this manually, just use a tool called 'aireplay-ng'.<br>
To do it just run on the terminal `aireplay-ng --deauth [big number for the number of deauthentication packets that will be sent] -a [MAC Address for the target network] -c [Client's MAC Address] [wireless adapter name]`. Bigger the number after `--deauth` longer the device will be disconnected (e.g. 1000000000), for 5GHz networks before the wireless adpter name use the flag `-D`.