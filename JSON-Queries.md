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