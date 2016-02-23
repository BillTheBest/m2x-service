# Guidelines for creating Limited <br />Client Libraries for M2X

This document aims to provide guidelines to organize the structure and
behavior of AT&T M2X client libraries for resource limited devices in order 
to keep them consistent with each other.

This document should be considered a subset of the original [Guidelines for M2X
Client Libraries](CLIENT-CONTRIBUTIONS.md). All guidelines discussed here are
specific for limited client libraries, but the original document contains the 
general expected behavior.

**Limited v. Full-Featured**

*Limited device*: device that cannot run Linux, hence requiring special bootloader to boot the device, e.g. Arduino, ARM mbed, Cypress PSoC, Teensy, etc.

*Full-featured device*: device that runs an embedded version of Linux, e.g. include Raspberry Pi, BeagleBoard, etc.

# Supported API methods

The implementation of limited M2X clients aims to provide support to restricted 
devices and therefore only a subset of the available endpoints should be 
supported by limited clients. These endpoints include:

1. Device creation: 
  > In order for physical devices to be able to initialize
themselves against M2X, the two endpoints that allow creating a device should
be supported.
  - [`POST /devices`](https://m2x.att.com/developer/documentation/v2/device#Create-Device)
  - [`POST /distributions/:id/devices`](https://m2x.att.com/developer/documentation/v2/distribution#Add-Device-to-an-existing-Distribution)

2. Stream creation:
  >  Devices must be able to create the streams they are going to
push data to.
  - [`PUT /devices/:id/streams/:name`](https://m2x.att.com/developer/documentation/v2/device#Create-Update-Data-Stream)

3. Values writing:
  - [`PUT /devices/:id/streams/:name/value`](https://m2x.att.com/developer/documentation/v2/device#Update-Data-Stream-Value)
  - [`POST /devices/:id/streams/:name/values`](https://m2x.att.com/developer/documentation/v2/device#Post-Data-Stream-Values)
  - [`POST /devices/:id/update`](https://m2x.att.com/developer/documentation/v2/device#Post-Device-Update--Single-Values-to-Multiple-Streams-)
  - [`POST /devices/:id/updates`](https://m2x.att.com/developer/documentation/v2/device#Post-Device-Updates--Multiple-Values-to-Multiple-Streams-)

4. Location updates:
  - [`PUT /devices/:id/location`](https://m2x.att.com/developer/documentation/v2/device#Update-Device-Location)

5. Time API:
  - [`GET /time`](https://m2x.att.com/developer/documentation/v2/time)

# M2X MQTT Documentation

Please review the AT&T M2X MQTT Documentation for additional information:
https://m2x.att.com/developer/documentation/v2/mqtt
