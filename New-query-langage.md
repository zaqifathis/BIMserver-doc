BIMserver has had several ways of querying the stored models, but none have been very useful so far. This page will describe the requirements of a new query language that should replace all the other ways of querying data.

Requirements

- Should be easy to read/write, or easy to build higher-level languages on top of it
- Query by type (e.g. IfcDoor), with or without subtypes
- Query on exact values of fields (e.g. guid = "FHAJJAJJH", oid=20020)
- Use comparative expressions like >, <
- Use functions like substr etc...
- An efficient implementation should be possible (using indices, not loading the complete model in advance)
- Should basically be possible to create a query to get any sub-graph of any given model
- Should have the possibility to traverse a model (recursively)
- Should allow for having reusable pieces of query that are used a lot
- Should have the possibility to simplify for example the concept of Ifc properties via IfcPropertySet etc...

## Possible standards/influences
- http://www.jsoniq.org/
- XQuery
- OQL

## Current preload query in BIMvie.ws

This is not very intuitive, but can be used to query a model quite precisely.

The "defines" section declares reusable query-parts, the "queries" section the actual queries (which are all joined as OR)

The first query get's all IfcProject objects (usually just one). For every IfcProject, 2 includes are traversed. "IsDecomposedByDefine" will follow the "IsDecomposedBy" field, for every object it will follow "RelatedObjects", it will then recursively call itself, and "ContainsElementsDefine" and "Representation". And so on... This will basically read the whole decomposes-tree, with some sidesteps.

This example script is used in BIMvie.ws to preload the minimal amount of objects needed to create the tree/types/classifications/layers tabs on the left.

```javascript
var preLoadQuery = {
	defines: {
		Representation: {
			field: "Representation"
		},
		ContainsElementsDefine: {
			field: "ContainsElements",
			include: {
				field: "RelatedElements",
				include: [
					"IsDecomposedByDefine",
					"ContainsElementsDefine",
					"Representation"
				]
			}
		},
		IsDecomposedByDefine: {
			field: "IsDecomposedBy",
			include: {
				field: "RelatedObjects",
				include: [
					"IsDecomposedByDefine",
					"ContainsElementsDefine",
					"Representation"
				]
			}
		}
	},
	queries: [
	    {
			type: "IfcProject",
			include: [
				"IsDecomposedByDefine",
				"ContainsElementsDefine"
			]
	    },
	    {
	    	type: "IfcRepresentation",
	    	includeAllSubtypes: true
	    },
	    {
	    	type: "IfcProductRepresentation"
	    },
	    {
	    	type: "IfcPresentationLayerWithStyle"
	    },
	    {
	    	type: "IfcProduct",
	    	includeAllSubTypes: true
	    },
	    {
	    	type: "IfcProductDefinitionShape"
	    },
	    {
	    	type: "IfcPresentationLayerAssignment"
	    },
	    {
	    	type: "IfcRelAssociatesClassification",
	    	include: [
	    		{
	    			field: "RelatedObjects"
	    		},
	    		{
	    			field: "RelatingClassification"
	    		}
	    	]
	    },
	    {
	    	type: "IfcSIUnit"
	    },
	    {
	    	type: "IfcPresentationLayerAssignment"
	    }
	]
};
```

## JSON Based Query Language

Query on type
```
{
  type: "IfcProject"
}
```

Query on oid
```
{
  oid: 12345
}
```

Query on oids (OR)
```
{
  oids: [12346, 56789]
}
```

Query on GUID
```
{
  guid: "EBEBEBEBE"
}
```

Query on GUID's (OR)
```
{
  guids: ["EBEBEBEBEB", "CDCDCDCDCD"]
}
```

Using AND, OR, XOR
```
{
  or: [{
    type: "IfcWall"
  }, {
    type: "IfcWallStandardCase"
  }]
}
```
