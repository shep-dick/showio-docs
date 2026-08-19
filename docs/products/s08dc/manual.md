# ShowIO Digital Combo 8

*Product Number: SIO-S08DC*

4-channel digital input + 4-channel digital output module.

- See the Quick Start Guide [here](../../products/s08dc/quick_start_guide.md)
- Download the PDF datasheet [here](../../assets/datasheet_s08dc.pdf)

## Introduction

The ShowIO Digital Combo 8 (SIO-S08DC) is a compact I/O node for show control and automation application. It provides 4 digital inputs and 4 digital outputs, controllable and configurable over Ethernet using the OSC protocol.

### What's in the Box
- ShowIO Digital Combo 8 Module (including enclosure, if ordered)
- Quick start QR card

### Intended Applications

ShowIO nodes are designed for live entertainment environments, where you need to: 

- **Trigger show cues** from physical buttons or sensors
- **Control loads** such as relays, solenoids, or valves
- **Integrate interactive effects** into your show

### Key Features

| Feature | Description| 
| --- | --- |
| 4 digital inputs | Isolated 12-24VDC sensing with configurable event messaging |
| 4 digital outputs | 2A per channel with overcurrent protection |
| OSC control | Native OSC communication for easy integration with show systems |
| Simple configuration | DIP switches for quick IP addressing (no software required for basic setup) |
| Robust protection | Overcurrent, overvoltage, reverse polarity, and ESD protection on all channels |
| Onboard testing | Pushbuttons and LEDs to test channels without a controller |

## Safety

!!! warning "Electrical Safety Warning"

    **READ AND UNDERSTAND ALL SAFETY INSTRUCTIONS BEFORE INSTALLATION OR USE**

    - This device operates at 12-24 volts DC and outputs up to 2A per channel. Improper installation or use may result in electric shock, fire, equipment damage, or personal injury.
    - Do not use this device in safety-critical applications where failure could result in injury, death, or significant property damage without implementing appropriate redundancy and fail-safe systems.
    - Installation and wiring must be performed by qualified personnel only, in accordance with local electrical codes and regulations.
    - Always disconnect power before making any connections or modifications to the device.
    - Do not exceed the rated voltage or current specifications. Each output channel is rated for 2A continuous current maximum. The power input is rated for 3A continuous current maximum.
    - The 3A fuse provides overcurrent protection for the device but does not replace proper circuit protection at the power source.
    - Ensure proper wire gauge and insulation for all connections. Use only copper conductors rated for the application.
    - This device must be installed in a suitable enclosure to protect against environmental hazards and accidental contact with live circuits.
    - Verify correct polarity before applying power. Reverse polarity may damage the device despite built-in protection.
    - Keep the device away from water, excessive heat, and flammable materials.

    **FAILURE TO FOLLOW THESE WARNINGS MAY RESULT IN SERIOUS INJURY OR DEATH**

## Technical Specifications

### Power Supply

Power can be supplied to the ShowIO node via the DC Power Input terminal block. There are two terminals for V+, and two terminals for 0V, internally connected. The DC power input can handle 12 to 24 volts DC.

Additionally, the node can be powered via 5V USB for testing and configuration. When powered via USB, the digital output channels are disabled. 

#### Power Supply Selection

The power supply should be chosen based on the types of loads you intend to connect to the digital output channels. 

#### Circuit Protection

The power supply has the following protection measures. Refer to the product datasheet for more information.

| Protection Measure | Fault Description |
| --- | --- |
| Resettable Fuse | The resettable fuse will trip at 5 amps, limiting the current draw of the node. The fuse will sustain 3 amps draw without tripping. |
| Reverse Voltage Blocking | If a negative voltage is applied to (V+, 0V), the voltage is blocked from being applied to the rest of the node. | 
| Overvoltage Crowbar | If the supply voltage exceeds safe limits, the resettable fuse will trip. |

### Digital Inputs

#### Electrical Model

<p align="center"><img src="../../../assets/diagrams/channel_models/digital_input_base.svg" height=200></p>

Each digital input channel drives an optoisolator inside the node. The input is totally isolated from the rest of the node; it only needs a positive voltage across the two terminals to trigger the channel.

### Digital Outputs

#### Electrical Model

<p align="center"><img src="../../../assets/diagrams/channel_models/digital_output_base.svg" height=200></p>

Each digital output channel is driven by a load controller that includes a P-channel MOSFET. The MOSFET sources from the node's DC power input. The 0V terminals provide a convenient location to connect a return path for a load, and are internally connected to the 0V terminals at the DC power input.

## Network Configuration

### DIP Switches

<p align="center"><img src="../../../assets/diagrams/dip_switches/base.svg" height=200></p>

### LAN Configuration

The ShowIO Digital Combo 8 uses onboard DIP switches to set its LAN (Local Area Network) configuration. Three configuration modes are available:

| Mode | DIP Switch State | Description |
| --- | --- | --- |
| **Quick-IP** | 1 to 254 | Use the DIP switches to set the last number in a static IP address on a factory-set subnet. |
| **Manual IP** | 0 | Manually set an IP address and subnet in software. |
| **Auto-IP (DHCP)** | 255 | Enable DHCP and receive an automatically assigned IP address from your network infrastructure. |

After making changes to a node's LAN configuration, power-cycle or restart it for the changes to take effect.

#### Setting the IP Address Manually

A node's static network settings can manually be set using commands from the [OSC API](../../osc_api/overview.md). Note that this requires an existing connection to the node. To enable manual IP mode, set the DIP switches to `0`. On next boot, the node will have the manually set IP configuration.

The factory-default manual IP setting is `10.11.12.10` with a subnet mask of `255.0.0.0` and default gateway `10.0.0.1`.

#### Setting the IP Address with Auto-IP

The node can use DHCP to request an automatically assigned IP address from a DHCP server (generally, a router or managed network switch). To enable DHCP, set the DIP switches to `255`. On next boot, the node will search for a DHCP server to request an IP address.

### OSC Configuration

After getting a node connected to a LAN, any Controller on that LAN can send it OSC commands at port `UDP: 8888` (configurable).

When a Controller sends a node a Request Command, the node will reply with a message sent to `UDP: 9999` (configurable).

### Status LED

Your node has an RGB LED beside the IO test buttons. It flashes yellow when the device is on but not connected to a LAN, and displays solid green when the device is on and connected to a LAN. 
