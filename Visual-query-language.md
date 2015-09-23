This page explains a visual query language. This will not necessarily become a real way of quering BIM models. For now it serves as tool to develop/explain a potential new query language.

# Current considerations
- Remove the "Root" node, if you consider all the blocks with no input's as starting points, there is no need to have a "Root" node.
- The condition blocks (gray blocks) seem to use a text-based expression, this is just a simplification. The actual query model will represent these with more building blocks such as "Equal", "Literal" etc...

# Examples

## Query a list of GUID's

Returns all IfcRoot (and subclasses) objects with the given GUID's (if they exist in the model). Of course these types of queries can also be done for "Name", "ObjectID" etc...

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/queryguids.png)

## Query multiple types

Queries all doors/windows, plus their subtypes, if any.

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/query2types.png)

## Query name property

Get all walls with name "Muur 1".

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/querynameproperty.png)

## Query AND + Comparators

This will return all IfcWall objects with a OverallWidth > 2 AND OverallHeight > 3

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/queryand.png)

## Query NOT + null

This will return all IfcWall objects that have a Representation. Could maybe also be visualized by adding an explicit NOT block.

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/querynotnull.png)

## Query IFC properties

These are not direct object-properties, but properties that are attached to the object via IfcPropertySet/IfcPropertySingleValue etc...

This functionality makes the query engine less schema-agnostic, another way of making it easier to query complex properties and also keep the query engine schema-less would be to use a [reusable query block](https://github.com/opensourceBIM/BIMserver/wiki/Reusable-query-%22Properties%22) for it, for example the [Properties](https://github.com/opensourceBIM/BIMserver/wiki/Reusable-query-%22Properties%22) block.

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/querycomplexproperties.png)

## Query object with certain property value, but exclude and get referenced

This query first selects all IfcBuildingStorey objects that have the name "Storey 2", which would usually be used to get one single storey (using a GUID here would be better). However this storey is not added to the resultset (note the "exclude" attribute). The Storey is only used as a path to get to the Window/Door objects that are linked to it.

The [Decomposes](https://github.com/opensourceBIM/BIMserver/wiki/Reusable-query-%22Decomposes%22) and [Contains](https://github.com/opensourceBIM/BIMserver/wiki/Reusable-query-%22Contains%22) blocks are uses of [reusable query blocks](https://github.com/opensourceBIM/BIMserver/wiki/Reusable-query-blocks). These blocks will recurse through the decomposes and contains relations. The objects encountered on the way also excluded (in this case).

Finally the IfcDoor and IfcWindow objects are selected, those are included in the results.

![](https://raw.githubusercontent.com/opensourceBIM/BIMserver/master/Documentation/img/query1storeywindowsanddoors.png)


