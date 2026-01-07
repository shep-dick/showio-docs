# Set Digital Input Event Message
Configures a custom OSC message to be sent to subscribers when a digital input state changes.  

!!! warning
    
    Event messages have an encoded size limitation of 128 bytes.

### Address
```
/sio/cfg/eventmsg/di/{channel}/set
```
...where {channel} is a single character channel number.

### Payload
- Arg 0 (`int` | `float` | `True` | `False`): Input state trigger (0/false for off, 1/true for on)
- Arg 1 (`string` | `blob`): Address of new event message. Example: "/cue/20/go"
- Arg 2+ (OPTIONAL - `any`): After the required arguments, up to 10 optional arguments provided in this
configuration message will be packed into the new event message.  

## Effects
Stores a custom OSC message in the device configuration. When the specified digital input channel changes to the specified state, the custom message will be sent to all registered subscribers.

## Example
Message: /sio/cfg/eventmsg/di/3/set T, /fader1/set, 255

- Arg 0 (True): this event message will trigger when the digital input changes state to True
- Arg 1 (string): the event message will have an address of "/fader1/set"
- Arg 2 (int): the event message will include an integer argument of 255

## Supported Devices

- ShowIO PROTO5