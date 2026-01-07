# OSC API Reference

Auto-generated documentation for OSC functions.

## Configuration Commands

These OSC commands allow the user to reconfigure the ShowIO device.

---
### Get Device Config
> **Function:** `get_cnfg`  
> **Source:** `cfg.rs`

> ⚠️ NOTE: WILL BE DEPRECATED ONCE DEVICE CONFIG GETS TOO BIG TO FIT IN A UDP PACKET (or I figure out a cleverer way to do this)

Queries the device configuration.
#### Address: `/sio/cfg/get`
#### Payload: none

### Response
#### Address: `/sio/cfg`
#### Payload:
- Arg 0 (`string`): Device configuration JSON object

---
### Set Device Config
> **Function:** `set_cfg_from_json`  
> **Source:** `cfg.rs`

> ⚠️ NOTE: WILL BE DEPRECATED ONCE DEVICE CONFIG GETS TOO BIG TO FIT IN A UDP PACKET (or I figure out a cleverer way to do this)

Overwrites the device configuration.
#### Address: `/sio/cfg/set`
#### Payload:
- Arg 0 (`string` | `blob`): Device configuration JSON object

### Effects
Overwrites device configuration with the JSON object. If the JSON is an invalid device configuration, the existing configuration will not be overwritten.

---
### Wipe Device Config
> **Function:** `wipe_config`  
> **Source:** `cfg.rs`

Resets the device configuration to factory defaults.
#### Address: `/sio/cfg/wipe`
#### Payload: none

### Effects
Overwrites the entire device configuration with the default initialization values.

---
### Get Config Section - Device ID
> **Function:** `get_device_id`  
> **Source:** `cfg.rs`

Queries the device ID configuration section.
#### Address: `/sio/cfg/deviceid/get`
#### Payload: none

### Response
#### Address: `/sio/cfg/deviceid`
#### Payload:
- Arg 0 (`string`): Device ID JSON object

---
### Set Config Section - Device ID
> **Function:** `set_device_id`  
> **Source:** `cfg.rs`

Overwrites the device ID configuration section.
#### Address: `/sio/cfg/deviceid/set`
#### Payload:
- Arg 0 (`string` | `blob`): Device ID JSON object

### Effects
Overwrites device ID configuration section with the JSON object. If the JSON is invalid, the existing configuration will not be overwritten.

---
### Get Config Section - Metadata
> **Function:** `get_metadata`  
> **Source:** `cfg.rs`

Queries the metadata configuration section.
#### Address: `/sio/cfg/metadata/get`
#### Payload: none

### Response
#### Address: `/sio/cfg/metadata`
#### Payload:
- Arg 0 (`string`): Metadata JSON object

---
### Set Config Section - Metadata
> **Function:** `set_metadata`  
> **Source:** `cfg.rs`

Overwrites the metadata configuration section.
#### Address: `/sio/cfg/metadata/set`
#### Payload:
- Arg 0 (`string` | `blob`): Metadata JSON object

### Effects
Overwrites metadata configuration section with the JSON object. If the JSON is invalid, the existing configuration will not be overwritten.

---
### Get Config Section - Local IP
> **Function:** `get_local_ip`  
> **Source:** `cfg.rs`

Queries the local IP configuration section.
#### Address: `/sio/cfg/localip/get`
#### Payload: none

### Response
#### Address: `/sio/cfg/localip`
#### Payload:
- Arg 0 (`string`): Local IP JSON object

---
### Set Config Section - Local IP
> **Function:** `set_local_ip`  
> **Source:** `cfg.rs`

Overwrites the local IP configuration section.
#### Address: `/sio/cfg/localip/set`
#### Payload:
- Arg 0 (`string` | `blob`): Local IP JSON object

### Effects
Overwrites local IP configuration section with the JSON object. If the JSON is invalid, the existing configuration will not be overwritten.

---
### Get Config Section - OSC
> **Function:** `get_osc`  
> **Source:** `cfg.rs`

Queries the OSC configuration section.
#### Address: `/sio/cfg/osc/get`
#### Payload: none

### Response
#### Address: `/sio/cfg/osc`
#### Payload:
- Arg 0 (`string`): OSC JSON object

---
### Set Config Section - OSC
> **Function:** `set_osc`  
> **Source:** `cfg.rs`

Overwrites the OSC configuration section.
#### Address: `/sio/cfg/osc/set`
#### Payload:
- Arg 0 (`string` | `blob`): OSC JSON object

### Effects
Overwrites OSC configuration section with the JSON object. If the JSON is invalid, the existing configuration will not be overwritten.

---
### Set Response Port
> **Function:** `set_response_port`  
> **Source:** `cfg.rs`

Sets the UDP port number used for OSC response messages.
#### Address: `/sio/cfg/responseport/set`
#### Payload:
- Arg 0 (`int` | `float`): UDP port number for responses

### Effects
Updates the device configuration to send all OSC response messages to the specified port.

---
### Subscribe Me
> **Function:** `subscribe_me`  
> **Source:** `cfg.rs`

Adds an endpoint to the list of subscribers that receive event notifications.
#### Address: `/sio/sub/me`
#### Payload:
- Arg 0 (OPTIONAL - `int` | `float`): Port number of the subscriber, if necessary

### Effects
Registers the source endpoint as a subscriber. If sent over network, the subscriber will be added as either TCP or UDP, depending on the source protocol, and the
subscriber's socket address will be the source IP and the supplied port. If a port is not supplied, it will default to the configured response port. If a subscription
request is sent over USB, the port is not necessary.
The device will send OSC event messages (e.g., digital input changes) to all registered subscribers. Returns an error if the subscriber is already registered or
the maximum number of subscribers is reached.

---
### Unsubscribe
> **Function:** `unsubscribe_me`  
> **Source:** `cfg.rs`

Removes an endpoint from the list of event notification subscribers.
#### Address: `/sio/unsub/me`
#### Payload:
- Arg 0 (OPTIONAL - `int` | `float`): Port number of the subscriber to remove

### Effects
Removes the source from the subscriber list, with the specified port number (if necessary). If a request is received from a UDP source with no specified port, it will default to trying the configured response port. Returns an error if the endpoint is not in the subscriber list.

---
### Provision Serial Number
> **Function:** `provision_serial_number`  
> **Source:** `cfg.rs`

Sets the device serial number in EEPROM.
#### Address: `/sio/cfg/serial/set`
#### Payload:
- Arg 0 (`string`): Serial number to write

### Effects
Writes the provided serial number to the device's EEPROM storage. This is typically used during device provisioning.

---
### Set Digital Input Event Message
> **Function:** `set_di_event_message`  
> **Source:** `cfg.rs`

Configures a custom OSC message to be sent to subscribers when a digital input state changes.
#### Address: `/sio/cfg/eventmsg/di/{channel}/set`
#### Payload:
- Arg 0 (`int` | `float` | `True` | `False`): Input state trigger (0/false for off, 1/true for on)
- Arg 1 (`string | blob`): Address of new event message. Example: "/cue/20/go"
- Arg 2+ (OPTIONAL - ANY): After the required arguments, up to 10 optional arguments provided in this
configuration message will be packed into the new event message.

NOTE: Event messages have an encoded size limitation of 128 bytes.

#### Example:
Message: /sio/cfg/eventmsg/di/3/set (T), (s)/fader1/set, (i)255
- Arg 0 (True): this event message will trigger when the digital input changes state to True
- Arg 1 (string): the event message will have an address of "/fader1/set"
- Arg 2 (int): the event message will include an integer argument of 255

### Effects
Stores a custom OSC message in the device configuration. When the specified digital input channel changes to the specified state, the custom message will be sent to all registered subscribers.

---
## Discovery Commands

These OSC commands allow clients to discover ShowIO devices on the network.

---
### Device Discovery
> **Function:** `handle_discovery_request`  
> **Source:** `discovery.rs`

Responds to a discovery request with device information including name, serial number, and port.
#### Address: `/sio/discover/request`
#### Payload:
- Arg 0 (`int` | `float`): Response port number

### Response
#### Address: `/sio/discovery/response`
#### Payload:
- Arg 0 (`string`): Device name
- Arg 1 (`string`): Serial number
- Arg 2 (`int`): UDP receive port

---
## I/O Commands

These OSC commands control and query the digital I/O channels.

---
### Set Digital Output
> **Function:** `set_digital_output`  
> **Source:** `io.rs`

Sets the state of a digital output channel.
#### Address: `/sio/do/{channel}/set`
#### Payload:
- Arg 0 (`int` | `float` | `True` | `False`): Output state (0/false for off, non-zero/true for on)

### Effects
Changes the state of the specified digital output channel (1-4).

---
### Get Digital Output
> **Function:** `get_digital_output`  
> **Source:** `io.rs`

Queries the current state of a digital output channel.
#### Address: `/sio/do/{channel}/get`
#### Payload: none

### Response
#### Address: `/sio/do/{channel}`
#### Payload:
- Arg 0 (`int`): Output state (0 for off, 1 for on)

---
### Get Digital Input
> **Function:** `get_digital_input`  
> **Source:** `io.rs`

Queries the current state of a digital input channel.
#### Address: `/sio/di/{channel}/get`
#### Payload: none

### Response
#### Address: `/sio/di/{channel}`
#### Payload:
- Arg 0 (`int`): Input state (0 for low, 1 for high)

---
### Get All Digital Inputs
> **Function:** `get_all_di_state`  
> **Source:** `io.rs`

Queries the current state of all digital input channels.
#### Address: `/sio/di/get`
#### Payload: none

### Response
#### Address: `/sio/di`
#### Payload:
- Arg 0 (`int`): Channel 1 state (0 for low, 1 for high)
- Arg 1 (`int`): Channel 2 state (0 for low, 1 for high)
- Arg 2 (`int`): Channel 3 state (0 for low, 1 for high)
- Arg 3 (`int`): Channel 4 state (0 for low, 1 for high)

---
## Utility Commands

These OSC commands provide utility functions for debugging and testing.

---
### Ping
> **Function:** `ping_handler`  
> **Source:** `misc.rs`

Responds to a ping request with a pong message, echoing back the provided arguments.
#### Address: `/ping`
#### Payload:
- Arg 0 (any): Message ID to echo back
- Arg 1 (any): Additional data to echo back

### Response
#### Address: `/pong`
#### Payload:
- Arg 0 (any): Echoed message ID from request
- Arg 1 (any): Echoed additional data from request

---
### Default Handler
> **Function:** `default_handler`  
> **Source:** `misc.rs`

Fallback handler for OSC messages that don't match any registered route. Logs the message address and arguments for debugging.
#### Address: (any unmatched address)
#### Payload: (any)

### Effects
Logs the received message address and argument count to the debug output.

---