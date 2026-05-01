# Ethernet and the Internet Protocol Guide

Low-level network technologies can get complicated quickly. However, you can set up a fairly large show control network if you have a handle on a few crucial topics. This is a quick guide to tell you what you need to know to get your ShowIO nodes onto your network. For more information, I recommend John Huntington's [Introduction to Show Networking](https://www.controlgeek.net/bookinfo).

## Ethernet
Ethernet is a wired networking technology used for computer-to-computer communication. You have likely used a CAT5, coaxial, or fiber optic cable to connect to a modem, ONT, or router implementing the Internet Protocol over Ethernet. You may even have hooked up a lighting console to set up an Art-Net network, implementing DMX512 over Ethernet. 

Ethernet is an *OSI Layer 2* or *Data Link Layer* protocol. It defines how data is transferred over *Layer 1,* the *Physical Layer.* Ethernet systems send data as frames, chunks of data with clearly defined beginnings, endings, and error-checking information. For a concrete comparison, Ethernet is like the Postal Service. Its job is to determine how to best get a piece of mail from point A to point B without the letter getting lost or damaged. The copper wire, fiber optic cable, or radio waves are the roads that the Post will send their mail carriers along. ShowIO nodes all implement Ethernet over twisted pair wires, aka any network cable with an 8P8C (or RJ45) jack on the ends. Ethernet also defines several possible sizes of network, although a Local Area Network (or LAN) is all that is likely to be relevant to a ShowIO implentation.  

## Internet Protocol (IP)

The Internet Protocol is the *OSI Layer 3* protocol that Show Technologies uses to send show control messages. Layer 3, the *Network Layer,* defines how the various computers and show control devices on a network address one another. ShowIO nodes use *IPv4,* the most commonly implemented version of the Internet Protocol. IPv4 consists of 2-part packets: a header with addressing info, and a payload. The addresses in the header are the most important concept for setting up a ShowIO network. You're likely familiar with an IP address; the Internet Protocol sets the rules for how those are assigned. An IPv4 address consists of four "octets," or 8-bit binary numbers. These are typically represented as 4 decimal equivalents separated with a period (*quad-dotted notation*), because `192.168.1.100` is easier to read than `11000000` `10101000` `00000001` `01100100`. To continue the mail metaphor from above, the Internet Protocol is the scheme by which every building in a town is assigned a mailing address so the Postal Service (the Ethernet Protocol) knows where to deliver the mail. The most important thing to remember is not to reuse addresses within a network.

Above the Internet Protocol is *Layer 4,* the *Transport Layer.* This defines how the payload in an Internet Protocol message is packaged, and, such as with TCP, may also come with its own error detection scheme. Open Sound Control messages (see the OSC Guide [here](../references/osc_guide.md),) exist above the transport layer, and define how applications will interpret Layer 4 messages.

## LANs

A *LAN,* or Local Area Network, is the smallest type of computing network that is likely to be relevant to your show control system. A LAN connects devices in a relatively small area like a theatre, home, or office building. A LAN may or may not be connected to a larger network like a MAN (Metropolitan Area Network) or WAN (Wide Area Network) that spans cities or large geographical regions, and may include smaller networks like a PAN (Personal Area Network), but configuring these is outside of what one would reasonably need to manage to set up a show control system. 

A LAN is defined by its physical reach, but the number of devices that can communicate on network is defined by the IP addresses assigned to the components on the network. Devices can only send messages to addresses that are on the same "Subnet." A subnet is a range of IP addresses that share some number of *Most Significant Bits.* The most significant digits of an IP address are the leftmost numbers. Remember that even though an IP address is written as 3 digit decimal numbers, the computer interprets each of those is an 8-bit binary number. The number of bits that must match for a subnet is defined by a *Subnet Mask.* The subnet mask may be written in quad-dotted notation like an IP address. For example, a subnet where the 24 most significant bits must match is written as `255.255.255.0` (equivalent to `11111111` `11111111` `11111111` `00000000`). It can also be written with a forward slash followed by the number of matching digits; the 24-bit subnet mask above could be written as `/24`. This notation generally follows an IP address, so an IP address on a `/24` subnet might be `192.168.1.100/24`. The slash-number format is known as *CIDR notation*. The computer at that address can communicate with a ShowIO device using the IP address `192.168.1.101/24`, but could NOT communicate with a lighting console at `192.168.2.102` because of the mismatch in the third octet. 

It is possible to communicate between subnets using a router. A router can be the internet router you use for your home WiFi, but some managed network switches (discussed below) can route between networks and/or subnets. 

## Addressing

When setting up a show control network, determining and recording the IP addresses you plan to use is one of the first and most important steps you can take. There are multiple ways to assign IP addresses to devices on a network. The simplest to explain is manually setting static IP addresses for every device on the network. This is a simple and reliable way to ensure that you always know what devices are communicating (as long as you've documented which device has which IP address!) with minimal risk of a configuration change breaking your network in the future. Devices can also automatically request an IP address from a central computer using a *DHCP Server* or *Link-Local Addressing*. No matter how you choose to do it, recording as much information as possible will help you and any collaborators during future integration and troubleshooting.

### Manual Addressing

If you choose to assign addresses manually, it may be tempting to start at `0.0.0.0` and work your way up. However, `0.0.0.0` is in one of several already defined IP address ranges. `0.0.0.0/8` is used by devices waiting to receive an IP address using an automatic configuration software. Other addresses you should avoid:

 Address Range | Special Assignment 
---------------|--------------------
 0.0.0.0/8| "This host on this network," a.k.a. automatic configuration 
 127.0.0.0/8| Loopback, a.k.a. a device communicating with itself 
 255.255.255.255| Broadcast, a.k.a. sending to the entire network

There are several ranges of IP addresses that are predefined by the Internet Engineering Task Force that you should avoid. *Special-Purpose IP Address Registries* can be found [here](https://www.rfc-editor.org/rfc/rfc6890#section-2.2.2). It will be quicker to provide three ranges of addresses that are reserved to be non-routable, making them perfect for show control networks that will never need to touch the open internet directly. Notice that the descending size of each subnet hints at the scale of network each range is designed to accomodate, from largest to smallest:

| Address Range |
|---------------|
| 10.0.0.0/8 |
|172.16.0.0/12|
|192.168.0.0/16|

Elsewhere in the docs, you will typically see examples written using addresses in the '192.168.0.0/16' range. 

Windows, Mac OS, Linux machines, and mobile devices all have their own ways to set static IP addresses. Each should have their own guide. Instructions to configure a ShowIO node's IP address manually can be found in [your device's](../products/overview.md) quick start guide.

If you choose to set your network up with manual IP addresses, the bare minimum documentation you should create is a table that lists all your devices and their respective addresses. This will help you when you are configuring show control software, ensure you don't set duplicate IP addresses, and give you a starting point for collaborating with other people who may have devices on the same network. It will also reduce the chances of using duplicate addresses by mistake. Adding two devices with the same IP address will cause problems, as devices on the network will not know what device to send to. A basic example of an IP table might look like this:

| Device | Address | Use |
| -------- | -------- | -------- |
| PC 1 | 192.168.1.10 | Main Control Machine |
| ShowIO Node 1 | 192.168.1.21 | Room 1 Props Control |
| ShowIO Node 2 | 192.168.1.22 | Room 2 Props Control |
| ShowIO Node 3 | 192.168.1.23 | Room 3 Props Control |

### DHCP Addressing

Many devices, including ShowIO nodes, can request and receive IP addresses automatically from a central computer running a *DHCP Server*. The server will provide a unique IP address to each device on the subnet, saving configuration time and guaranteeing that no two devices have the same address. When a device has been off the network for long enough, the DHCP Server may reassign its address to a new machine. This makes it less likely that you will run out of space in your subnet, but if your show control program is not able to keep up with the changing addresses, it may send messages to the wrong device. 

Most computers will be set to use DHCP-assigned addresses by default, requesting and receiving an address from a network switch with a built in DHCP server. Instructions to configure a ShowIO node to use DHCP in [your device's](../products/overview.md) quick start guide.

If using DHCP, you should still plan to record the subnet that you are using for your show control network for all the reasons stated above.

### LAN Physical Connections

A typical show control network being used to control ShowIO devices over ethernet will consist of a control PC and one or more ShowIO nodes connected to a network switch with CAT5 cable. The computer may be a laptop or desktop, or could be a dedicated show control machine like a lighting console. You will simply set all the devices with unique IP addresses on the same subnet (manually or using DHCP), plug them all into the network switch, and they will start communicating over Ethernet. Voilà! If they don't, double check:
 * Network cable connections
 * I.P. address sassignments
 * Subnet information
 * Show control software configuration

Your choice of network switch may matter. Even the most basic off-the-shelf network switch will be capable of assigning IP addresses over DHCP and ensuring that messages get from device to device, but may have limitations. For instance, most basic switches use Energy Efficient Ethernet, an "enhancement" to standard ethernet wherein transmission is shut down during periods of inactivity. This could lead to loss of data if a ShowIO node tries to send while the switch isn't expecting data. Additionally, your standard network switch will be *unmanaged*, meaning it has few to no configuration options. A *managed switch* will allow you to use powerful network configuration tools like VLANs, which allows you to fully separate subnets that are running through the same switch to and prioritize certain traffic. Some manufacturers even make show control-specific managed switches which will have configuration options for things like running audio or video data in addition to show control messages through the same switch. Configuring such switches is beyond the scope of this guide, but may be worth looking into as your network demands grow.