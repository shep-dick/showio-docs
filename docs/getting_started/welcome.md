# Getting Started

Welcome to the docs! We're glad to have you here.  

If you're new, we recommend at least skimming this section of the documentation before diving in to making cool stuff with your ShowIO gear.  

## What is ShowIO?

ShowIO is our family of show control hardware. By using a ShowIO device, you can connect stuff to your show control system that normally wouldn't fit. How do you plug a hall effect sensor into your Mac to get it to trigger a sound cue? How do you make your lightboard turn on a pneumatic valve? ShowIO is how.  

A ShowIO device is called a **Node**. Nodes have I/O ports, to connect **Instruments** (which is what we'll call any electrical device like sensor, switch, motor, valve, etc), and communication ports, to connect to **Controllers** and other Nodes. Information for specific nodes can be found in the [Products](../products/overview.md) section.

A Controller can be anything that sends messages to a ShowIO Node. For example - a Mac running QLab, an ETC Eos lighting console, or an iPad running TouchOSC.  

## Connecting ShowIO

### Ethernet
ShowIO Nodes use an Ethernet link to connect to Controllers. Ethernet-based networking is fast, flexible, reliable, and widely adopted.  

For more information about how to get an Ethernet connection set up, read our [Ethernet Guide](../references/ethernet_guide.md)

### USB
ShowIO Nodes also support USB communication, which makes it easy to connect to a **Node** with no configuration if you don't need the speed or flexible topology of Ethernet - just plug and play!

### OSC
All ShowIO products have first-class support for Open Sound Control (OSC). OSC is a show control protocol that most manufacturers implement in one way or another due to its simplicity and efficiency. Read our [OSC Guide](../references/osc_guide.md) to learn more about the protocol.  

### The ShowIO API
OSC is only a message format - the protocol doesn't specify any messages or functions, or even how to send messages. That's why we've created the [ShowIO API](../osc_api/overview.md), which defines the common language and rules that ShowIO Nodes use when sending and receiving OSC messages — what messages exist, what data they carry, and what each Node will do in response.

Here's how the pieces fit together:

| Ethernet/USB                     | OSC                                        | ShowIO API                                  |
| -------------------------------- | ------------------------------------------ | ------------------------------------------- |
| The connection between devices   | Universal show control message format      | The commands, data, and behaviors shared    |

