This page should reflect the current status of BIMserver features

If you test a functionality and it works, but it says "test" in this table, please let us know and we will update this document. If you are missing features, please let us know too. If you do not agree on certain decisions, also please let us know! If you want to adopt a feature, well you get the idea...

| Feature | Status | Future plans |
| ------------- | ------------- | ----- | ------ | 
| CityGML Serializer | Not working | Move to own repository |
| Collada Serializer| Not working | Move to own repository |
| Clash Detection | Not working, has been removed from Bonsma Engine | Remove entirely, maybe move BCF classes to Shared |
| BIMQL | Working, but not as documented (e.a. no geometry) | Decide whether to improve/fix or create a new query language |
| SceneJS Serializers | Not working, not updated | Remove entirely, not used anymore for SceneJS-based tools (BIMsurfer, BIMvie.ws) |
| Java Query Engine | Working | Remove entirely, not used, too complex, inefficient, easier to write a plugin |
| AdminGUI | Working | Remove, all functionalities available in BIMvie.ws |
| Charting | Working | Move to own repository |
| JavaModelChecker | Working | Remove, same reason as JavaQueryEngine |
| FileBasedObjectIDM | Remove, all ObjectIDM stuff will be removed, and replaced by better Query engine |
| IfcEngine | Working | Move to own repository |
| XSLT Serializer | Unknown|Remove, not used, inefficient |
| IFC 2x3tc1 Step Serializer | Working | Stable |
| IFC 4 Step Serializer | Working | Stable |
| IFC 2x3tc1 XML Serializer | Unknown | Test |
| IFC 4 XML Serializer | Unknown | Test |
| IFC 2x3tc1 Step Deserializer | Working | Stable |
| IFC 4 Step Deserializer | Working | Stable |
| IFC 2x3tc1 XML Deserializer | Unknown | Test |
| IFC 4 XML Deserializer | Unknown | Test |
| Basic Model Merger | Unknown | Test |
| GUID Based Model Merger | Unknown | Test |
| Name Based Model Merger | Unknown | Test |
| Sending Emails | Working | Remove, never seen a database server that sends emails |
| JSON API | Working | Stable |
| SOAP API | Unknown | |
| Protocol Buffers API | Unknown | |
| org.bimserver.database.query.conditions.* | Working | Will be removed in favor of a new query language |
| Database migrations | Working | Stable |
| BimServerClient Library | Working | Stable |
| LowLevelCalls | More tests required | |
| JAR Starter | Working | Stable |
| WAR Build | Working | Stable |
| Generating Geometry | Working | Stable |
| Logging of events | Not working | Update |
| Plugin Manager | Working | Stable |
| Running services | Working | Stable, but not intuitive |
| console.html | Working | Not all features implemented, needs an update |
| User/rights management | Not fully implemented | Check all actions |
| IFC Schema | Working | Will remove as plugin and integrate directly because there is only one implementation and interface is (too) large |