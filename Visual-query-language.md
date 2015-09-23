This page explains a visual query language. This will not necessarily become a real way of quering BIM models, for now it serves as tool to develop/explain the new query language.

# Current considerations
- Remove the "Root" node, if you consider all the blocks with no input's as starting points, there is no need to have a "Root" node.

# Examples

## Query a list of GUID's

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/queryguids.png)

## Query multiple types

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/query2types.png)

## Query name property

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/querynameproperty.png)

## Query AND + Comparators

This will return all IfcWall objects with a OverallWidth > 2 AND OverallHeight > 3

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/queryand.png)

## Query NOT + null

This will return all IfcWall objects that have a Representation. Could maybe also be visualized by adding an explicite NOT block.

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/querynotnull.png)

## Query IFC properties

These are not direct object-properties, but properties that are attached to the object via IfcPropertySet/IfcPropertySingleValue etc...

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/querycomplexproperties.png)

## Query object with certain property value, but exclude and get referenced

This query first selects all IfcBuildingStorey objects that have the name "Storey 2", which would usually be used to get one single storey (using a GUID here would be better). However this storey is not added to the resultset (note the "exclude" attribute). The Storey is only used as a path to get to the Window/Door objects that are linked to it.

The [Decomposes](https://github.com/opensourceBIM/BIMserver/wiki/Reusable-query-%22Decomposes%22) and [Contains](https://github.com/opensourceBIM/BIMserver/wiki/Reusable-query-%22Contains%22) blocks are uses of reusable blocks.

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/query1storeywindowsanddoors.png)



