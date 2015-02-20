# Guidelines for creating a new M2X Client Library

This document aims to provide some guidelines to organize the structure and behavior of AT&T M2X's client libraries in order to keep them consistent with each other. Please make sure to consult the [AT&T M2X API Documentation](https://m2x.att.com/developer/documentation/) if you have questions about AT&T M2X API functionality. 

## Documentation
- All libraries should have the same [introduction](CLIENT-INTRODUCTION.md) in their `README.md` file and should include a copy of the standard [CONTRIBUTING.md](https://github.com/attm2x/m2x-ruby/blob/master/CONTRIBUTING.md) in their repository
- The rest of the `README.md` file should provide:
  - Installation instructions.
  - A brief introduction on how the library is to be used.
  - An example of usage.
  - An explanation on the versioning strategy, using [Semantic Versioning 2.0.0](http://semver.org/) if possible.
  - License notes.

Example: https://github.com/attm2x/m2x-ruby/blob/master/README.md

## About releases
Each client library release should include a [git tag](http://git-scm.com/book/en/v2/Git-Basics-Tagging) with the corresponding version number.

Ready to use binaries should be made available for users when applicable. The correct procedure depends on the platform:
- If there is a centralized library repository (e.g. Rubygems for Ruby), the library should be pushed there.
- If the library needs to be compiled (e.g. Java), use [Github's release API](https://help.github.com/articles/creating-releases/) and upload the compiled files there. _Note that this supersedes the need to create version tags since they will already be created by it._

## User Agent
All libraries should pass their user agent to the M2X API, using the following format: `M2X-<Platform>/<Version> <language>/<language_version> (operative_system)`.

For example: `M2X-Ruby/2.0.0 ruby/2.1.3 (x86_64-darwin14.0)`

## Content type
Currently, all data is sent and received as JSON, libraries should include the correct content type of `application/json` when performing requests with a JSON payload.

## Accept header
The `accept` header should be included, with `application/json` as its value.

## General behavior
The idea behind this section is to standardize client libraries as much as possible. The following guidelines should be followed when the programming language and platform allows so. In other cases, try to stick to this behavior as much as possible but deviate where necessary.

### Class naming
Declare classes following the conventions of the [M2X documentation](https://m2x.att.com/developer/documentation/overview). Ideally the following classes should be declared:
  - Distribution
  - Device
  - Stream
  - Key

Each class should implement all the methods defined in their corresponding documentation.

### Method signature
Non-CRUD methods should be named after their corresponding endpoint when possible (For example: `Stream#stats`). A special case are the methods that publish stream values:
- `Stream#update_value`: For posting a single value to a Stream.
- `Stream#post_values`: For posting multiple values to a Stream.
- `Device#post_updates`: For posting multiple values (and, optionally, location) to multiple streams of a Device.

_Note: Using CamelCase or underscore convention in the method names should be done according to the programming language standard, and not to the specification on this guide._

### Parameters validation
Client libraries **should not** validate parameters sent to the API. Relying on the API for validating the parameters allows us to change them when necessary without the need to update the libraries.

### Response status codes validation
Avoid validating API response status codes. If validation is necessary, try to allow all `2xx` codes for success, and `4xx` or `5xx` codes for error instead of specific codes.

### API Responses
A `Response` class should be instantiated to represent all API responses. This class should expose the following methods:
  - `raw`: The raw response body.
  - `json`: The parsed response body.
  - `status`: The status code of the response.
  - `headers`: The headers included on the response.
  - `success?`: Whether response `status` is a success (status code `2xx`)
  - `client_error?`: Whether response `status` is one of `4xx`
  - `server_error?`: Whether response `status` is one of `5xx`
  - `error?`: Whether `client_error?` or `server_error?` is true

### Last Response
When possible, a reference to the last received response should be saved on the `Client` object

### Example
Refer to the [M2X-Ruby](https://github.com/attm2x/m2x-ruby) client library for an example.

### MQTT
If you are developing a client library that interacts with the M2X API MQTT endpoint, please refer to the [Guidelines for M2X MQTT Client Libraries](MQTT-CLIENT-CONTRIBUTIONS.md)
