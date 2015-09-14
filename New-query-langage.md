BIMserver has had several ways of querying the stored models, but none have been very useful so far. This page will describe the requirements of a new query language that should replace all the other ways of querying data.

Requirements

- Should be easy to read/write, or easy to build higher-level languages on top of it
- Query by type (e.g. IfcDoor)
- Query on exact values of fields (e.g. guid = "FHAJJAJJH")
- Query on 
- An efficient implementation should be possible (one using indices, not loading the complete model)