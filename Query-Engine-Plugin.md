#summary How to write Query engine plugins

A Query Engine makes it possible for users to query the BIMserver.

{{{
public interface QueryEnginePlugin extends Plugin {
	/**
	 * @return A usable QueryEngine implementation
	 */
	QueryEngine getQueryEngine();
	
	/**
	 * @return Return a list of keys (usually file names) corresponding to code examples for this plugin
	 */
	Collection<String> getExampleKeys();
	
	/**
	 * @param key
	 * @return Return the code example for the given key
	 */
	String getExample(String key);
}
}}}

{{{
public interface QueryEngine {
	/**
	 * @param model The complete model
	 * @param code The query, represented as a string
	 * @return RunResult
	 */
	IfcModelInterface query(IfcModelInterface model, String code, Reporter reporter, ModelHelper modelHelper) throws QueryEngineException;
}
}}}