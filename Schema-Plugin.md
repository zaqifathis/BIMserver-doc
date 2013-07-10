#summary How to write Schema plugins

A schema plugin provides the calling code with information about a schema. There is currently only one implementation, and that one can read an express schema file.

{{{
public interface SchemaPlugin extends Plugin {
	SchemaDefinition getSchemaDefinition();
	File getExpressSchemaFile();
}
}}}