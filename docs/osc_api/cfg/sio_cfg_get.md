# Get Device Config
Get a JSON string of the device configuration.  
    
**Address:** `/sio/cfg/get`  
**Payload:** none  

> ⚠️ NOTE: WILL BE DEPRECATED ONCE DEVICE CONFIG GETS TOO BIG TO FIT IN A UDP PACKET (or I figure out a cleverer way to do this)

## Response
**Address:** `/sio/cfg`  
**Payload:**   

* [0] (`string`): Device configuration JSON object