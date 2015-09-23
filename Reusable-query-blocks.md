Reusable query blocks can be used to simplify query building and to make them more readable.

IFC is a complex schema, and uses a lot of relation objects, traversing them can be easier by using reusable query blocks.

Elements of a reusable query block:
- IN
- Initial type query (right after IN), selects the types it can work with, basically determines that allowed IN connections
- OUT

# List of reusable query blocks
- [Decomposes](https://github.com/opensourceBIM/BIMserver/wiki/Reusable-query-%22Decomposes%22)
- [Contains](https://github.com/opensourceBIM/BIMserver/wiki/Reusable-query-%22Contains%22)
- [DecomposesContains](https://github.com/opensourceBIM/BIMserver/wiki/Reusable-query-%22DecomposesContains%22)
- [Properties]()