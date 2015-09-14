BIMserver has had several ways of querying the stored models, but none have been very useful so far. This page will describe the requirements of a new query language that should replace all the other ways of querying data.

Requirements

- Should be easy to read/write, or easy to build higher-level languages on top of it
- Query by type (e.g. IfcDoor), with or without subtypes
- Query on exact values of fields (e.g. guid = "FHAJJAJJH", oid=20020)
- Use comparative expressions like >, <
- Use functions like substr etc...
- An efficient implementation should be possible (using indices, not loading the complete model in advance)
- Should basically be possible to create a query to get any sub-graph of any given model
- Should have the possibility to traverse a model

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