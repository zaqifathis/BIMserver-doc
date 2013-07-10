#summary How to write Serializer plugins

A serializer serializes an object model to a stream of data. Among the default serializers are: IFC2x3, IfcXml, CityGML and others. Most serializers will output a textbased format but that is not required.

Serializer plugins must implement org.bimserver.plugins.serializers.SerializerPlugin interface
{{{
public interface SerializerPlugin extends Plugin {
	Serializer createSerializer(); // The actual method that will create a serializer. Have a look at subclasses of EmfSerializer to see how to build one
	String getDefaultExtension(); // A default extension, the user can change this
	String getDefaultContentType(); // A default contentType, the user can change this
}
}}}

{{{
public interface Serializer {
	void init(IfcModelInterface model, ProjectInfo projectInfo, PluginManager pluginManager, IfcEngine ifcEngine) throws SerializerException;
	void writeToFile(File file) throws SerializerException;
	byte[] getBytes();
	IfcModelInterface getModel();
	InputStream getInputStream() throws IOException;
	void writeToOutputStream(OutputStream outputStream) throws SerializerException;
}
}}}

You can subclass EmfSerializer so you don't have to implement all methods.