# HZP4 - Metadata server

## Data model

Metadata server uses postgresql as backend database. The data model is defined in the following diagram:

```plantuml
```
{src = "puml/metadata-server/Core_Schema.puml"}

## Resource types

The supported resource types in MS are handled by loosely couple modules,
each resource type handler has its own metadata schema that may be only understood 
by the handler itself.

### Json resource

Json resource stores json data and optionally provides data schema for validation.

#### Definition schema

Embedded definition schema

```json
{
  "name": "example",
  "type": "json",
  "schema_def": {
    "type": "embeded",
    "properties": {
      "schema": "data_schema_in_json"
    }
  },
  "enable_validaion": "true|false"
}
```

Apicurio definition schema

```json
{
  "name": "example",
  "type": "json",
  "schema_def": {
    "type": "apicurio",
    "properties": {
      "url": "apicurio_api_url",
      "artifact": "artifact_name"
    }
  },
  "enable_validaion": "true|false"
}
```

#### Data schema

```text
syntax = "proto3"
Struct jsonValue = 1
```

## Architecture

```plantuml
```
{src = "puml/metadata-server/Architecture.puml"}



























