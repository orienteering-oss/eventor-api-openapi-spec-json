# eventor-api-openapi-spec-json

[![Travis build status](https://app.travis-ci.com/orienteering-oss/eventor-api-openapi-spec-json.svg?branch=main)](https://travis-ci.com/github/orienteering-oss/eventor-api-openapi-spec-json)

:warning: **NB:** this is an unofficial JSON version of the API. See
[orienteering-oss/eventor-api-openapi-spec](https://github.com/orienteering-oss/eventor-api-openapi-spec)
for an unofficial XML version (that is closer / equal to the official version of
the API).

JSON version of the OpenAPI spec / Swagger for the Eventor API:
[openapi.yml](./openapi.yml).

You can browse the
[Swagger UI](https://orienteering-oss.github.io/eventor-api-openapi-spec-json)
for this spec, but it will not work because of CORS. You can use it to browse
and create cURL commands that you can execute in your own terminal. Or you could
import the OpenAPI spec into Postman and make your calls from there.

**What is Eventor?** Eventor is the event system for
[orienteering](https://en.wikipedia.org/wiki/Orienteering) races in different
countries, so if you want to arrange an orienteering event, you will probably
register it in your local Eventor system to make other people see it and for
them to register to your event (and where you can upload results after the event
is done).

## Usage of the Eventor API

To use the Eventor API, you need an API key.

The different Eventor websites are:

- [Norwegian Eventor](https://eventor.orientering.no/)
- [Swedish Eventor](https://eventor.orientering.se/)
- [Australian Eventor](https://eventor.orienteering.asn.au/)
- [International Eventor](https://eventor.orienteering.org/)

Add `/api/documentation` to either of the URLs to get the documentation for that
particular Eventor website (the documentation is also included in the OpenAPI
specification).

## How did I create this

I have previously manually assembled
[an OpenAPI spec for the Eventor API](https://github.com/orienteering-oss/eventor-api-openapi-spec/blob/main/openapi.yml)
with the XML content in mind. I have also previously converted the IOF v3 XSD
into a
[JSON Schema](https://github.com/orienteering-oss/iof-orienteering-data-schemas/blob/main/iof_v3_schema.json)
with Jackson (see repo
[iof-orienteering-data-schemas](https://github.com/orienteering-oss/iof-orienteering-data-schemas#datastandard-v3)).
So I followed [a guide](https://blog.stoplight.io/openapi-json-schema) on how to
convert JSON schema to OpenAPI spec, using the
[openapi-contrib/json-schema-to-openapi-schema](https://github.com/openapi-contrib/json-schema-to-openapi-schema)
JavaScript library. This gave me a new file containing the IOF v3 JSON Schema as
an OpenAPI spec. Then I copied this into the `components` section of the
existing OpenAPI spec, and started using the correct `$ref`s for request bodys
and responses.

## See also

- Almost all data returned from the API is specified in IOF JSON schema v3, see
  this and XML version of the same spec in
  [orienteering-oss/iof-orienteering-data-schemas](https://github.com/orienteering-oss/iof-orienteering-data-schemas)
- Java helper library for converting XML from Eventor to JSON objects (and
  back):
  [orienteering-oss/iof-xml](https://github.com/orienteering-oss/iof-xml). It is
  actually this library that does the converting behind the scenes for this
  version of the API.
- GraphQL version of the Eventor API:
  [mikaello/eventor-graphql-api](https://github.com/mikaello/eventor-graphql-api)
