#### Channel Wiring Example

<p align="center"><img src="../../../assets/diagrams/wiring/digital_input.svg" height=200></p>

#### Setting the IP Address with Quick-IP

This configuration flow should be familiar to anyone that's set a DMX address on a light. We set the first 8 DIP switches to a binary representation of a number, 1-254.

!!! tip

    If you're not familiar with binary notation, check out this [helpful article from Laserworld](https://www.laserworld.com/en/laserworld-toolbox/dmx-address-setting.html) about setting an address using DIP switches. They even have a handy calculator!

ShowIO products ship with Quick-IP defaults `192.168.10.x` on a `255.255.255.0` subnet, where `x` is the 1-254 number set using the DIP switches. The Quick-IP address prefix, subnet, and gateway are software-configurable via OSC.

For example, to set the Quick-IP to 192.168.10.**10**, you would set the second and fourth DIP switches to get the binary number `0000 1010`, or decimal 10.

<p align="center"><img src="../../../assets/diagrams/dip_switches/example_ip.svg" height=200></p>

##### Quick-IP Example

Alice has (3) ShowIO Nodes that she wants to connect to a network. She sets her laptop to `192.168.10.10` with a subnet mask of `255.255.255.0` and a default gateway of `192.168.10.1`. She sets the DIP switches on her three ShowIO Nodes to `30`, `31`, and `32`. She plugs all her devices into a network switch, and the network looks like:

| Device | IP Address |
| --- | --- |
| Alice's Laptop | 192.168.10.10 |
| Node #1 | 192.168.10.30 |
| Node #2 | 192.168.10.31 |
| Node #3 | 192.168.10.32 |

Now Alice can send messages from her laptop to all three nodes!