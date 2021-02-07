A serializer serializes an object model to a stream of data. Among the default serializers are: IFC2x3, IfcXml, CityGML and others. Most serializers will output a textbased format but that is not required.

Serializer plugins must implement [SerializerPlugin](../blob/master/PluginBase/src/org/bimserver/plugins/serializers/SerializerPlugin.java) interface.

```java
public interface SerializerPlugin extends Plugin {
	Serializer createSerializer(PluginConfiguration plugin);
	Set<Schema> getSupportedSchemas();
	String getOutputFormat(Schema schema);
	Set<String> getRequiredGeometryFields();
}
```

```java
public interface Serializer {
	void init(IfcModelInterface model, ProjectInfo projectInfo, boolean normalizeOids) throws SerializerException;
	void writeToOutputStream(OutputStream outputStream, ProgressReporter progressReporter) throws SerializerException;
}
```

You can subclass [EmfSerializer](../blob/master/PluginBase/src/org/bimserver/plugins/serializers/EmfSerializer.java) so you don't have to implement all methods.

You can subclass [AbstractGeometrySerializer](../blob/master/PluginBase/src/org/bimserver/plugins/serializers/AbstractGeometrySerializer.java) if your serializer is going to need triangulated geometry.

