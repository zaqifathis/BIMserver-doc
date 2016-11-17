> The new query language is still in development, so expect this to change.

You can read the original motivations to write this language [here](https://github.com/opensourceBIM/BIMserver/wiki/New-query-langage)

# Intro

Some characteristics to of this language to keep in mind:
- The data model of the "queried" is the same data model as the "query results". In most cases it will be Ifc2x3tc1 or Ifc4
- The previous also explains why there are no aggregates, because there is no place to store those
- A query result is always a subset of the original model
- Query language is probably not the best term here, a "filter language" might be better
- The queries are based on objects. Geometry is not treated any other way. If you don't ask for geometry, you won't get it.

# JSON

All queries must be valid JSON. This means that all keys must be quoted, all strings must be quoted. When you send your query to BIMserver via the [ServiceInterface.download](https://thisisanexperimentalserver.com/apps/console?interface=ServiceInterface&method=download) call via JSON, make sure to base64 encode your query.

[Downloading models](https://github.com/opensourceBIM/BIMserver/wiki/Downloading-models)

# Base query

This query will query all objects.

```json
{
}
```

# Type query

This query will get all IfcWall objects
```json
{
  "type": "IfcWall"
}
```

When your model for example only contains IfcWallStandardCase objects, this query will not return any objects, although IfcWallStandardCase is a subtype of IfcWall. To include subtypes, you have to explicitly define this:

```json
{
  "type": "IfcWall",
  "includeAllSubtypes": true
}
```

# GUID query

When you already know the GUID(s) of (an) object(s), you can query those directly:
```json
{
  "guids": ["GUID1", "GUID2"]
}
```

# OID query

The same as for GUIDs, you can also query by OID (ObjectID)
```json
{
  "oids": [1523, 2130, 898]
}
```

