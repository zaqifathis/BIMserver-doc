To connect to a BIMserver you can use one of the 3 protocols: [SOAP](SOAP), [JSON](JSON API) or [Protocol Buffers](Protocol Buffers). To make connecting to a BIMserver even easier, there also is a Java library you can use.

# Get the client library

From version 1.5 on we are using Maven for all dependency management. We suggest you do too when using the BIMserver Client library as it makes installing all the required dependencies a lot easier.

You can find the Maven XML snippet in the latest release notes (for example https://github.com/opensourceBIM/BIMserver/releases/tag/parent-1.5.51). Make sure you match the version of the client with the version of your BIMserver. It  looks something like this:
```xml
<dependency>
    <groupId>org.opensourcebim</groupId>
    <artifactId>bimserverclientlib</artifactId>
    <version>1.5.51</version>
</dependency>
```

Of course you can also use the client from source code, in that case download a source zip file, or checkout the projects from GIT.

# Examples

```java
import java.io.File;
import java.io.IOException;

import org.bimserver.client.json.JsonBimServerClientFactory;
import org.bimserver.emf.IfcModelInterface;
import org.bimserver.emf.MetaDataManager;
import org.bimserver.interfaces.objects.SDeserializerPluginConfiguration;
import org.bimserver.interfaces.objects.SProject;
import org.bimserver.models.ifc2x3tc1.IfcWall;
import org.bimserver.plugins.PluginException;
import org.bimserver.plugins.PluginManager;
import org.bimserver.plugins.services.BimServerClientException;
import org.bimserver.plugins.services.BimServerClientInterface;
import org.bimserver.shared.BimServerClientFactory;
import org.bimserver.shared.ChannelConnectionException;
import org.bimserver.shared.PublicInterfaceNotFoundException;
import org.bimserver.shared.UsernamePasswordAuthenticationInfo;
import org.bimserver.shared.exceptions.ServiceException;

/**
 * @author Ruben de Laat
 * 
 * This example shows how to connect to a remote BIMserver, using the bimserver-client-download (a bunch of JAR files you have to link in your IDE)
 * Make sure you actually link the JAR files in you IDE (in eclipse add to build-path), otherwise the PluginManager won't find certain plugins
 *
 */
public class ClientLibDownloadExample {
	public static void main(String[] args) {
		try {
			// Define the home directory, this is the base for the extracted plugins and more
			File home = new File("home");

			if (!home.exists()) {
				home.mkdir();
			}

			// Client-side, we also use a PluginManager, for example to be able to use the (IFC) schemas
			PluginManager pluginManager = new PluginManager(new File(home, "tmp"), System.getProperty("java.class.path"), null, null, null);
			
			// Load all plugins available on the classpath
			pluginManager.loadPluginsFromCurrentClassloader();
			
			// Initialize all loaded plugins
			pluginManager.initAllLoadedPlugins();

			// Create a MetaDataManager, and initialize it, this code will be simplified/hidden in the future
			MetaDataManager metaDataManager = new MetaDataManager(pluginManager);
			pluginManager.setMetaDataManager(metaDataManager);	
			metaDataManager.init();

			// Create a factory for BimServerClients, connnect via JSON in this case
			BimServerClientFactory factory = new JsonBimServerClientFactory(metaDataManager, "http://localhost:8080");
			
			// Create a new client, with given authorization, replace this with your credentials
			BimServerClientInterface client = factory.create(new UsernamePasswordAuthenticationInfo("admin@bimserver.org", "admin"));

			SProject project = client.getBimsie1ServiceInterface().addProject("test" + Math.random(), "ifc2x3tc1");

			// Look for a deserializer
			SDeserializerPluginConfiguration deserializer = client.getBimsie1ServiceInterface().getSuggestedDeserializerForExtension("ifc", project.getOid());
			
			// Checkin file
			client.checkin(project.getOid(), "test", deserializer.getOid(), false, true, new File("C:/Git/BIMserver2/TestData/data/AC11-Institute-Var-2-IFC.ifc"));
			
			// Refresh project
			project = client.getBimsie1ServiceInterface().getProjectByPoid(project.getOid());
			
			// Load model without lazy loading (complete model at once)
			IfcModelInterface model = client.getModel(project, project.getLastRevisionId(), true, false);
			
			System.out.println(model.getAllWithSubTypes(IfcWall.class).size());
		} catch (PluginException e) {
			e.printStackTrace();
		} catch (ServiceException e) {
			e.printStackTrace();
		} catch (ChannelConnectionException e) {
			e.printStackTrace();
		} catch (BimServerClientException e) {
			e.printStackTrace();
		} catch (PublicInterfaceNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```
Examples on how to use the client-library can be found [here](https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/serviceinterface).

Examples on how to use the client-side EMF model can be found [here]( https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/emf)

Examples on how to use the low-level-calls from the client library are [here](https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/lowlevel)