A serializer serializes an object model to a stream of data. Among the default serializers are: IFC2x3, IfcXml, CityGML and others. Most serializers will output a textbased format but that is not required.

Serializer plugins must implement org.bimserver.plugins.serializers.SerializerPlugin interface
```java
public interface SerializerPlugin extends Plugin {
	/**
	 * @return A serializer
	 */
	Serializer createSerializer(PluginConfiguration plugin);

	/**
	 * @return Whether this plugin will be needing geometry
	 */
	boolean needsGeometry();
}
```

```
public interface Serializer {
	void init(IfcModelInterface model, ProjectInfo projectInfo, PluginManager pluginManager, RenderEnginePlugin renderEnginePlugin, boolean normalizeOids) throws SerializerException;
	void writeToFile(File file) throws SerializerException;
	byte[] getBytes();
	IfcModelInterface getModel();
	InputStream getInputStream() throws IOException;
	void writeToOutputStream(OutputStream outputStream) throws SerializerException;
	void reset();
}
```

You can subclass [EmfSerializer](../blob/master/Shared/src/org/bimserver/plugins/serializers/EmfSerializer.java?source=c) so you don't have to implement all methods.

You can subclass [AbstractGeometrySerializer](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/plugins/serializers/AbstractGeometrySerializer.java?source=cc) if your serializer is going to need triangulated geometry.