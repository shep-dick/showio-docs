# First Steps

This is where you should start if you've just received a ShowIO node and are ready to start designing effects. This guide is not designed for any specific show control software; for specific integrations, take a look at the cookbooks *here.*

## A Note On Safety

ShowIO devices are very powerful, but they are not designed for safety-critical applications. Always be thoughtful about how you are designing your system: if an errant "go" cue could drop something heavy on an audience member, a ShowIO node is likely not the controller you want to use. 

## Designing Your System

Before you start designing a ShowIO effect, it will be helpful to consider how you want to control and configure your system. Consider the following questions:

* How many devices need to communicate on this show control network?
* What software(s) will interface with your ShowIO nodes?
* Will you use [Ethernet](../references/ethernet_guide.md) or USB to transmit OSC messages? Ethernet will require more setup, but allows for larger networks and more communicative. USB requires only one wire, but many show control programs do not natively support OSC over USB.
* If using Ethernet, will you set IP addresses [manually](../references/ethernet_guide.md#manual-addressing) or [automatically](../references/ethernet_guide.md#dhcp-addressing)?
    * What [network and subnet](../references/ethernet_guide.md#lans) is your control computer on? Can you change those easily? If not, consider putting your ShowIO devices on your computer's LAN rather than changing everything.

Once you've answered those questions, I recommend writing down some of the basic information in a table. Even if you only have one computer and one node, it will save you from having to dig for IP addresses or COM port assignments, and will make your system easy to grow in the future. That may look something like:

| Device | IP Address | RX Port | Description |
| -------- | -------- | -------- | -------- |
| Computer | 192.168.10.10/16 | 9999 | Show Control Primary Computer |
| Node 1 | 192.168.10.100/16 | 8888 | ShowIO Node |

!!! tip

    Notice that the first three octets of these IP addresses match—see the [Ethernet Guide](../references/ethernet_guide.md#lans) for why that is.

!!! tip "Bonus Tip"
    ShowIO devices come pre-configured on the 192.168.10.0/24 subnet. Setting your computer to this subnet before you connect your ShowIO devices will make them truly plug-and-play.

Or:

| Device | USB Port | Description |
| -------- | -------- | -------- |
| Computer | N/A | Show Control Primary Computer |
| Node 2 | COM2 | ShowIO Node |

!!! tip

    Different operating systems use different naming conventions for their USB ports.

You may also wish to draw a diagram of how you plan to connect your devices together. If you only plan to connect one node to one computer this may be unnecessary, but as your networks grow such diagrams become invaluable. The more you have planned and recorded before you connect your devices, the less time you'll have to spend chasing networking errors.

## Plugging In

You can power your ShowIO node two ways: USB-C into the jack on the data side, or 12-24v DC into the IO side. USB-C power ONLY powers the ShowIO node microchip; you can configure the device and transmit OSC messages, but you can't run IO off of it. Connecting the node to DC power will both power up both the chip and the IO. 

!!! warning "Electrical Safety Warning"

    **SEE FULL WARNINGS IN YOUR DEVICE'S MANUAL**

    - Improper installation or use may result in electric shock, fire, equipment damage, or personal injury.
    - Always disconnect power before making any connections or modifications to the device.
    - Ensure proper wire gauge and insulation for all connections. Use only copper conductors rated for the application.
    - Verify correct polarity before applying power. Reverse polarity may damage the device despite built-in protection.
    - Keep the device away from water, excessive heat, and flammable materials.

Once you're powered up, you should see the status LED turn yellow (if you're not connected to Ethernet) or green (if you are) and you can start pushing buttons and watching lights turn on. If you're planning to use OSC over Ethernet, you should configure your device's DIP switches to use a QuickIP or DHCP and plug it into the network switch.

