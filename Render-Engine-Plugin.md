#summary How to write Render Engine plugins

A Render Engine makes it possible to convert an IFC file to triangulated geometry.

{{{
public interface RenderEnginePlugin extends Plugin {
	RenderEngine createIfcEngine(PluginConfiguration pluginConfiguration) throws RenderEngineException;
}
}}}

{{{
public interface RenderEngine {
	RenderEngineModel openModel(File ifcFile) throws RenderEngineException;
	RenderEngineModel openModel(InputStream inputStream, int size) throws RenderEngineException;
	RenderEngineModel openModel(byte[] bytes) throws RenderEngineException;
	void close();
	void init() throws RenderEngineException;
}
}}}