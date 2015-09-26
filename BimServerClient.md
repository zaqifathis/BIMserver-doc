To connect to a BIMserver you can use one of the 3 protocols: [SOAP](SOAP), [JSON](JSON API) or [Protocol Buffers](Protocol Buffers). To make connecting to a BIMserver even easier, there also is a Java library you can use.

# Get the client library

You can download a recent release from https://github.com/opensourceBIM/BIMserver/releases, and then the file named "bimserver-client-lib-[date].zip". Make sure it matches with your BIMserver version.

Extract the zipfile, copy the jar files from the "lib" and "dep" folders to your own project and include them in the build path.

Of course you can also use the client from source code, in that case download a source zip file, or checkout the projects from GIT.

# Examples

```java
import java.io.File;
import java.util.List;

import org.bimserver.LocalDevPluginLoader;
import org.bimserver.client.json.JsonBimServerClientFactory;
import org.bimserver.emf.IfcModelInterface;
import org.bimserver.emf.MetaDataManager;
import org.bimserver.interfaces.objects.SProject;
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
			// Client-side, we also use a PluginManager, for example to be able to use the (IFC) schemas
			PluginManager pluginManager = LocalDevPluginLoader.createPluginManager(new File("home"));
			
			// Create a MetaDataManager, and initialize it, this code will be simplified/hidden in the future
			MetaDataManager metaDataManager = new MetaDataManager(pluginManager);
			pluginManager.setMetaDataManager(metaDataManager);	
			metaDataManager.init();

			// Initialize all loaded plugins
			pluginManager.initAllLoadedPlugins();
			
			// Create a factory for BimServerClients, connnect via JSON in this case
			BimServerClientFactory factory = new JsonBimServerClientFactory(metaDataManager, "http://localhost:8080");
			
			// Create a new client, with given authorization, replace this with your credentials
			BimServerClientInterface client = factory.create(new UsernamePasswordAuthenticationInfo("admin@bimserver.org", "admin"));

			// Example code assuming at least 1 project in your BIMserver
			List<SProject> projects = client.getBimsie1ServiceInterface().getAllProjects(true, true);
			SProject project = projects.get(0);

			// Load a model
			IfcModelInterface model = client.getModel(project, project.getLastRevisionId(), false, false);
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
		}
	}
}
```
Examples on how to use the client-library can be found [here](https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/serviceinterface).

Examples on how to use the client-side EMF model can be found [here]( https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/emf)

Examples on how to use the low-level-calls from the client library are [here](https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/lowlevel)