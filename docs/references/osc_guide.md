# What is OSC?

OSC is a flexible, transportation-agnostic show control protocol. It is the foundation upon which ShowIO control networks are built. Much of the information on this page comes from [OpenSoundControl Specification](https://ccrma.stanford.edu/groups/osc/spec-1_0.html) by Matt Wright; please refer to that for a comprehensive explanation of how OSC works.

OSC is an endlessly configurable way to send information and commands to entertainment software and devices across various types of network. The OpenSoundControl list of OSC implementations is non-exhaustive but contains dozens of commonly used softwares, controllers, and programming languages. The ability to easily interface with seemingly disparate devices is why ShowIO uses OSC as the backbone of its control and communication. With only network and power connections and some OSC messages, a user can use a ShowIO node to read a sensor, trigger a sound and video cue in QLab, fire a lighting cue in EOS, and control a solenoid valve, all with minimal configuration and no need to "translate" for different programs.

## Anatomy of an OSC Message

An OSC message consists of three parts: an address, a type tag, and some number of arguments. An OSC message does not need an argument, but will have the other two items. Each piece is separated by null (`/0`) ASCII characters and padded out to a multiple of 4 bytes. The address defines the action a device should take upon receipt of the message, the type tag defines what information (if any) is associated with that action, and the argument is that information.

An OSC address defines the action a device should take upon receipt of the OSC message. It consists of a series of *OSC Address Patterns,* which are strings that start with a `/`. The last string in an OSC address is the *method*, this defines the action that the recipient should take upon receipt of the message. The preceding strings are *containers* which describe where and how the method should be invoked.

ShowIO API addresses always start with `/sio`. From there, an address will start with a broad definition of its function and get narrower with each OSC Address Pattern. For example, the OSC address for [SET MANUAL IP ADDRESS](../osc_api/configuration_commands/set_manual_ip_address.md) is:
>`sio/cfg/lan/manual/ip/set`

If we read the address from right to left (from most specific to least specific), we see that it is an OSC method to **set** an **IP** address as a **manual** override for a device's **LAN** **configuration** (cfg). All addresses in the ShowIO API are designed to be specific and descriptive.

A type tag, or *OSC Type Tag String* comes after the OSC address. It is a string of characters beginning with `,` that corresponds to the number and type of arguments in an OSC message. ShowIO devices support integers (`i`), floats (`f`), and strings (`s`). Returning to the [SET MANUAL IP ADDRESS](../osc_api/configuration_commands/set_manual_ip_address.md) command, we can see it takes 4 `ints` or `floats`. This means its type tag will be `,iiii`, `,ffff`, or any combination of 4 `i`'s and `f`'s.

An argument is data sent with an OSC message. In the ShowIO API, this can be used to turn an output on or off, set a configuration parameter, or even define an entirely new OSC message. The type tags define how many arguments of each type are included (down to zero arguments), and the arguments are delineated in the message with `/0` ASCII characters. If we look at a complete [SET MANUAL IP ADDRESS](../osc_api/configuration_commands/set_manual_ip_address.md) message with 4 integer arguments, we get:
>`/sio/cfg/lan/manual/ip/set ,iiii 192 168 020 120`

With null characters included, we read:
>`/sio/cfg/lan/manual/ip/set/0/0,iiii/0/0/0192/0168/0020/0120/0`

## Using OSC

Most show control programs support OSC in some form. There are several ways to get a ShowIO device talking to another program: configure that program to send and listen for messages from the ShowIO API, configure a ShowIO device to send custom messages formatted for the other program, or use an intermediary software to broker communication between a ShowIO device and one or more programs. If your intermediary is also a show control program, that method may be equivalent to the first. However, you may wish to explore software that doesn't have an entertainment focus. Check out the cookbook **link to cookbook here** for implementations with specific show control programs. 