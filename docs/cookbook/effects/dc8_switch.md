# CONNECT A BUTTON OR SWITCH TO YOUR /DIGITAL/COMBO/8

Start here if you want your ShowIO node to send messages when a button is pressed or switch is flipped.

[1. You Will Need](../effects/dc8_switch.md#1-you-will-need)

[2. Wiring Your Switch](../effects/dc8_switch.md#2-wiring-your-switch)

[3. Reading Your Switch](../effects/dc8_switch.md#3-reading-your-switch)

## 1. You Will Need

### Tools:
 - Small slotted screwdriver

### Equipment:
 - 12-24v DC Power Supply
 - Jumper Wire
 - Switch

!!! tip

    A switch refers to any device that opens or closes a circuit when manually operated. An arcade button is a momentary switch (because it operates "momentarily"). Switches may be Normally Open or Normally Closed depending on if they close or open the circuit when actuated; either will work with your ShowIO node. This guide will also work with anything that closes a circuit!

## 2. Wiring Your Switch

!!! warning "Electrical Safety Warning"
    - Always disconnect power before making any connections or modifications to the device.

- Jump the positive power terminal to the positive terminal of the input you want to control.
- Wire one leg of your switch to the ground power terminal.
- Wire the other leg of your switch to the ground input terminal.
- Connect your /digital/combo/8 to power. When you actuate your switch, the indicator LED for your selected input should turn on.

### Digital Input 1 Wiring Example

<p align="center"><img src="../../../assets/diagrams/wiring/digital_input.svg" height=200></p>

## 3. Reading Your Switch

Once your wiring is working, you will need to configure your show control software to read your /digital/combo/8's input messages. You can do this in one of two ways: polling or subscribing. Polling your device allows you to read the state of any or all of your digital inputs at any time by sending a status request OSC message. When you subscribe to a device, it will send messages whenever one of its input channels changes state. 

!!! tip

    Make sure your device is on the same subnet as your show control software before you try to send and receive messages! Refer to the [Quick Start Guide](../../products/s08dc/quick_start_guide.md#3-getting-on-the-network) for a fast method to get your computer and /digital/combo/8 talking.

### Polling Your Device

 - Review the API page for [`Get Digital Input`](../../osc_api/io_commands/get_digital_input.md) and [`Get All Digital Inputs`](../../osc_api/io_commands/get_all_digital_inputs.md). If you are polling more than one input, consider using `Get All Digital Inputs` as it will give you more data in fewer messages. Fewer messages means less network traffic, and less network traffic means faster response times!
 - Decide how frequently you want to poll your device. If you need near-instantaneous response time, you might consider sending a polling as frequently as every .05 seconds. If you are polling inputs for something less response-time-critical, consider how infrequently you can poll the device and still get the performance you require.
 - Configure your show control software to send either `Get Digital Input` or `Get All Digital Inputs` on a repeating interval based on your determinations above.
 - Configure your show control software to listen for the [response](../../osc_api/io_commands/get_digital_input.md#response) `/sio/di`.
 - Test your integration!

### Subscribing To Messages

- Review the API page for [`Subscribe Me`](../../osc_api/configuration_commands/subscribe_me.md), [`Unsubscribe Me`](../../osc_api/configuration_commands/unsubscribe.md), [`Add Subscriber`](../../osc_api/configuration_commands/add_subscriber.md), and [`Remove Subscriber`](../../osc_api/configuration_commands/remove_subscriber.md). There are a couple of ways to add and remove subscribers; if you want to receive messages using the same computer and software that you're using to configure your device, `Subscribe Me` and `Unsubscribe Me` are the easiest.
- Determine your control software's receiving port.
- Send a `Subscribe Me` OSC message to your node using your receiving port, or an `Add Subscriber` message using the target software's IP address and port.
- Configure your show control software to listen for the `response` *not yet in API docs!*
- Test your integration!
