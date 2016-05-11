# Guidelines for creating/contributing to <br />M2X Client Libraries

This document aims to provide some guidelines to organize the structure and behavior of AT&T M2X's client libraries in order to keep them consistent with each other. Please make sure to consult the [AT&T M2X API Documentation](https://m2x.att.com/developer/documentation/) if you have questions about AT&T M2X API functionality.

## Documentation

All libraries should have the following files in their repository:

- `README.md`, organized according to the following sections:
  - An [introduction](CLIENT-INTRODUCTION.md) section copied from the file in this repository.
  - Installation instructions.
  - A brief introduction on how the library is to be used.
  - An example of usage.
  - An explanation on the versioning strategy, using [Semantic Versioning 2.0.0](http://semver.org/) when possible.
  - License notes with a link to a `LICENSE` file (see below).

- `CONTRIBUTING.md` which links to the [contributing guidelines](CONTRIBUTING.md) on this repository.
- `LICENSE` file which is a copy of the [license file on this repository](LICENSE)

Documentation example: https://github.com/attm2x/m2x-ruby

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

Declare classes following the conventions of the [M2X documentation](https://m2x.att.com/developer/documentation/overview).

The following classes should be declared:
  - Collection
  - Command
  - Device
  - Distribution
  - Job
  - Key
  - Metadata
  - Stream

Each class should implement all the methods defined in their corresponding documentation, with the following exceptions:

  - Jobs
    - Only the View Job Details endpoint should be implemented

The following API's **should not** be added to client libraries:
  - Triggers
  - Charts

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

### Limited Clients

If you are developing a client library for a device with limited resources or one that interacts
with the M2X API MQTT endpoint, please refer to the [Guidelines for M2X Limited
Client Libraries](LIMITED-CLIENT-CONTRIBUTIONS.md)

*************************************************
### Client Libraries by Category/Maintainer

*Full-Featured*
- [C-HTTP](https://github.com/attm2x/m2x-c) @xxuejie
- [Python](https://github.com/attm2x/m2x-python) @omab
- [Ruby-HTTP](https://github.com/attm2x/m2x-ruby) @fsaravia
- [PHP-HTTP](https://github.com/attm2x/m2x-php) @jellehenkens
- [Node JS](https://github.com/attm2x/m2x-nodejs) @grilix
- [Tessel](https://github.com/attm2x/m2x-tessel) @netarc
- [JavaScript](https://github.com/attm2x/m2x-javascript) @grilix
- [Java](https://github.com/attm2x/m2x-java) @kristinpeterson
- [Android](https://github.com/attm2x/m2x-android) @kristinpeterson
- [iOS](https://github.com/attm2x/m2x-ios) @lucholaf
- [Elixir](https://github.com/attm2x/m2x-elixir) @jemc
- [Erlang](https://github.com/attm2x/m2x-erlang) @jemc
- [dot net](https://github.com/attm2x/m2x-dot-net) @inkel
- [Node Red](https://github.com/attm2x/node-red-m2x) @fsaravia
- [Go](https://github.com/jsgoecke/m2x-go) (Community Library)

*Limited Libraries*
- [Arduino rewrite](https://github.com/attm2x/m2x-arduino-rewrite) @netarc
- [Old Arduino](https://github.com/attm2x/m2x-arduino) @xxuejie
- [Launchpad Energia](https://github.com/attm2x/m2x-launchpad-energia) @xxuejie
- [mbed](https://github.com/attm2x/m2x-arm-mbed) @xxuejie
- [C-MQTT](https://github.com/attm2x/m2x-c-mqtt) @xxuejie
- [Cypress PSOC](https://github.com/attm2x/m2x-cypress-psoc) @xxuejie
- [Spark Core](https://github.com/attm2x/m2x-spark-core) @netarc
- [Electric Imp](https://github.com/attm2x/m2x-electric-imp) @xxuejie
- [Nanode](https://github.com/attm2x/m2x-nanode) @xxuejie
- [Ruby-MQTT](https://github.com/attm2x/m2x-ruby-mqtt) @fsaravia
- [PHP-MQTT](https://github.com/attm2x/m2x-php-mqtt) @jellehenkens
- [Python-MQTT](https://github.com/attm2x/m2x-python-mqtt)
- [mruby](https://github.com/attm2x/m2x-mruby) @jemc
- [Samsung Gear S](https://github.com/attm2x/m2x-gear-s)  @vsiul [Samsung]
- [Cylon.js](https://github.com/hybridgroup/cylon-m2x) (Community Library)
- [wot.io](https://github.com/WoTio/opifex.m2x) (Community Library)
