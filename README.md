# eventor-api-openapi-spec-json

[![Validate OpenAPI spec](https://github.com/orienteering-oss/eventor-api-openapi-spec-json/actions/workflows/validate.yml/badge.svg)](https://github.com/orienteering-oss/eventor-api-openapi-spec-json/actions/workflows/validate.yml)

**This is an experimental JSON model, not an API that serves JSON.**
The Eventor servers listed in [openapi.yml](./openapi.yml) return XML, as does
the current `eventor-proxy`.
The `application/json` responses and request bodies in this spec describe a
possible representation after local XML-to-JSON conversion; they do not describe
the media types returned or accepted by those servers.
Some operations in this spec still describe XML.

Use [eventor-api-openapi-spec](https://github.com/orienteering-oss/eventor-api-openapi-spec)
for the actual Eventor HTTP API and for generated clients.
This JSON spec has not been validated against a single converter or JSON-serving
proxy, so do not use it as an executable API contract.
Its [Swagger UI](https://orienteering-oss.github.io/eventor-api-openapi-spec-json)
is useful for browsing the proposed JSON shapes, but its "Try it out" requests
cannot return the JSON responses shown here.

**What is Eventor?**
Eventor is the event system for
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
- [International Eventor](https://eventor.orienteering.sport/) (previously `eventor.orienteering.org`, which still redirects)

Add `/api/documentation` to either of the URLs to get the documentation for that
particular Eventor website (the documentation is also included in the OpenAPI
specification).

## How did I create this

I have previously manually assembled
[an OpenAPI spec for the Eventor API](https://github.com/orienteering-oss/eventor-api-openapi-spec/blob/main/openapi.yml)
with the XML content in mind.
I have also previously converted the IOF v3 XSD
into a
[JSON Schema](https://github.com/orienteering-oss/iof-orienteering-data-schemas/blob/main/iof_v3_schema.json)
with Jackson (see repo
[iof-orienteering-data-schemas](https://github.com/orienteering-oss/iof-orienteering-data-schemas#datastandard-v3)).
So I followed [a guide](https://blog.stoplight.io/openapi-json-schema) on how to
convert JSON schema to OpenAPI spec, using the
[openapi-contrib/json-schema-to-openapi-schema](https://github.com/openapi-contrib/json-schema-to-openapi-schema)
JavaScript library.
This gave me a new file containing the IOF v3 JSON Schema as
an OpenAPI spec.
Then I copied this into the `components` section of the
existing OpenAPI spec, and started adding `$ref`s for request bodies
and responses.

The IOF JSON schema does not cover Eventor's native XML structures on endpoints
such as `/events` and `/entries`.
[iof-xml](https://github.com/orienteering-oss/iof-xml) converts standard IOF XML
to JSON, but its output has a document-type wrapper such as `{"resultList": {...}}`
that this spec does not model.
Unwrapped JAXB/Jackson output with null fields omitted validated against this
spec's `eventList` and `resultList` schemas for IOF XML responses from events
23452 and 24759.
[rescript-eventor](https://www.npmjs.com/package/rescript-eventor) parses several
native Eventor XML responses into its own typed records, with a different shape.
There is currently no converter known to produce this spec's JSON for every
endpoint.

## See also

- Standard IOF XML documents are defined by the
  [IOF data schemas](https://github.com/orienteering-oss/iof-orienteering-data-schemas).
- Native Eventor XML documents follow the [Eventor XSD](https://eventor.orientering.se/api/schema).
- Java helper library for converting standard IOF XML to JSON (and back):
  [orienteering-oss/iof-xml](https://github.com/orienteering-oss/iof-xml).
- GraphQL version of the Eventor API:
  [mikaello/eventor-graphql-api](https://github.com/mikaello/eventor-graphql-api)
