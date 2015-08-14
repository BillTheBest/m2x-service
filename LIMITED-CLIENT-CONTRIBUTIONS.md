# Guidelines for creating Limited Client Libraries for M2X

This document aims to provide guidelines to organize the structure and
behavior of AT&T M2X client libraries for resource limited devices in order 
to keep them consistent with each other.

This document should be considered a subset of the original [Guidelines for M2X
Client Libraries](CLIENT-CONTRIBUTIONS.md). All guidelines discussed here are
specific for limited client libraries, but the original document contains the 
general expected behavior.

# Supported API methods

The implementation of limited M2X clients aims to provide support to restricted 
devices and therefore only a subset of the available endpoints should be 
supported by limited clients. These endpoints include:

1. Device creation: In order for physical devices to be able to initialize
themselves against M2X, the two endpoints that allow creating a device should
be supported.
  - `POST /devices`
  - `POST /distributions/:id/devices`

2. Stream creation: Devices must be able to create the streams they are going to
push data to.
  - `PUT /devices/:id/streams/:name`

3. Values writing.
  - `PUT /devices/:id/streams/:name/value`
  - `POST /devices/:id/streams/:name/values`
  - `POST /devices/:id/updates`

4. Location updates.
  - `PUT /devices/:id/location`

# M2X MQTT Documentation

Please review the AT&T M2X MQTT Documentation for additional information:
https://m2x.att.com/developer/documentation/v2/mqtt
