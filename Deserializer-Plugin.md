#summary How to write Deserializer plugins

To deserialize a stream of data to an object model.

{{{
public interface DeserializerPlugin extends Plugin {
	Deserializer createDeserializer();
	boolean canHandleExtension(String extension);
}
}}}

{{{
public interface Deserializer {
	void init(SchemaDefinition requireSchemaDefinition);
	IfcModelInterface read(File file, boolean setOids) throws DeserializeException;
	IfcModelInterface read(InputStream inputStream, String fileName, boolean setOids, long fileSize) throws DeserializeException;
}
}}}

You can subclass EmfDeserializer so you don't have to implement all methods.