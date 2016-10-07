# Starting points
- There are two roles, any application can provide just one of the roles, or both of them
  - A: Software that sends data to other software (B)
    Examples: CAD software (using e.g. IFC export), A BIMserver (after a user checks in)
  - B: Software that receives data from other software (A)
    Examples: Simulation software, BIMserver (simply storing the data, or running services).
- Other than in the previous version, in this version, it should be possible to issue all communication from A. The main advantage being that no listening sockets have to be opened on A. This is useful on corporate networks (or even private networks) and when A is for example CAD software.
- A service describes which input and which output formats it supports
- All communication will be JSON. For two methods (sending and receiving data), there will be alternative methods that perform better
- All authentication will be done with OAuth2

# List of schemas
- Ifc2x3tc1
- Ifc4
- BCF1.0
- BCF2.0

# List of formats
- Step
- Xml

# Namespaces

| Short name | Content-Type | URL |
|---|---|---|
| IFC_STEP_2X3TC1 | application/ifc | http://www.buildingsmart-tech.org/specifications/ifc-releases/ifc2x3-tc1-release |
| IFC_STEP_4 | application/ifc | http://www.buildingsmart-tech.org/specifications/ifc-releases/ifc4-release |
| IFC_XML_2x3TC1 | application/ifcxml | http://www.buildingsmart-tech.org/specifications/ifcxml-releases/ifcxml2x3-release/summary |
| IFC_XML_4 | application/ifcxml | http://www.buildingsmart-tech.org/specifications/ifcxml-releases/ifcxml4-release/ifcxml4-release-summary |
| IFC_JSON_2x3TC1 | application/json | No formal specification |
| IFC_JSON_4 | application/json | No formal specification |
| IFC_JSON_GEOM_2x3TC1 | application/json | No formal specification |
| IFC_JSON_GEOM_4 | application/json | No formal specification |
| BCF_ZIP_1.0 | application/zip | http://www.buildingsmart-tech.org/specifications/bcf-releases/bcfxml-v1 |
| BCF_ZIP_2.0 | application/zip | https://github.com/BuildingSMART/BCF-XML |
| GLTF_1.0 | model/gltf+json | https://github.com/KhronosGroup/glTF/blob/master/specification/README.md |
| GLTF_BIN_1.0 | model/gltf.binary | https://github.com/KhronosGroup/glTF/blob/master/extensions/Khronos/KHR_binary_glTF/README.md |
| COLLADA_1.5 | model/vnd.collada+xml | https://www.khronos.org/files/collada_spec_1_5.pdf |
| KMZ_2.2.0 | application/vnd.google-earth.kml+xml .kml | http://schemas.opengis.net/kml/2.2.0/ |
| BINARY_GEOMETRY_6 | | No formal specification |
| CITYGML_2.0.0 | application/gml | https://portal.opengeospatial.org/files/?artifact_id=47842 |

- Setup OAuth
- Setup ServiceConfig
```java
long setData(String schema, byte[] data, String serviceConfigurationId);
Progress getProgress(long topicId);
byte[] getData(topicId);
ServiceDescriptor getServiceDescriptor(String serviceName);
```