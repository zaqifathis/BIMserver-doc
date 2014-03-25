To connect to a BIMserver you can use one of the 3 protocols: [SOAP](SOAP), [JSON](JSON API) or [Protocol Buffers](Protocol Buffers). To make connecting to a BIMserver even easier, there also is a Java library you can use.

# Get the client library

You can download a nightly build [here](http://archive.opensourcebim.org/BIMserver/nightly%20builds/), select the latest date, and then the file named "bimserver-client-lib-[date].zip". Or download a release.

Extract the zipfile, copy the jar files from the "lib" and "dep" folders to your own project and include them in the build path.

Of course you can also use the client from source code, in that case download a source zip file, or checkout the projects from GIT.

# Examples
Connecting via SOAP with authentication, and listing all projects

```java
	// Create a BimServerClientFactory, change Json to ProtocolBuffers or Soap if you like
	BimServerClientFactory factory = new SoapBimServerClientFactory("http://localhost:8080");
			
	// Create a new BimServerClient with authentication
	BimServerClient bimServerClient = factory.create(new UsernamePasswordAuthenticationInfo("admin@bimserver.org", "admin"));

        // List project names
	for (SProject project : bimServerClient .getBimsie1ServiceInterface().getAllProjects(true, true)) {
		System.out.println(project.getName());
	}

```

Connecting with JSON and checking in a file:
```java
	// Create a BimServerClientFactory, change Json to ProtocolBuffers or Soap if you like
	BimServerClientFactory factory = new JsonBimServerClientFactory("http://localhost:8080");

	// Create a new BimServerClient with authentication
	BimServerClientInterface bimServerClient = getFactory().create(new UsernamePasswordAuthenticationInfo("admin@bimserver.org", "admin"));

	// Create a new project
	SProject newProject = bimServerClient.getBimsie1ServiceInterface().addProject("New project name");
			
	// This is the file we will be checking in
	File ifcFile = new File("location of the file you want to checkin");
			
	// Find a deserializer to use
	SDeserializerPluginConfiguration deserializer = bimServerClient.getBimsie1ServiceInterface().getSuggestedDeserializerForExtension("ifc");
			
	// Checkin
	bimServerClient.checkin(newProject.getOid(), "test", deserializer.getOid(), false, true, ifcFile);

```

Connect via JSON and Download a revision as IFC
```java
	// Create a BimServerClientFactory, change Json to ProtocolBuffers or Soap if you like
	BimServerClientFactory factory = new JsonBimServerClientFactory("http://localhost:8080");

	// Find a serializer
	SSerializerPluginConfiguration serializer = bimServerClient.getBimsie1ServiceInterface().getSerializerByContentType("application/ifc");
			
	// Get the project details
	SProject project = bimServerClient.getBimsie1ServiceInterface().getProjectByPoid([INSERT OID OF YOUR PROJECT]);
			
	// Download the latest revision
	Long downloadId = bimServerClient.getBimsie1ServiceInterface().download(project.getLastRevisionId(), colladaSerializer.getOid(), true, false); // Note: sync: false
	InputStream downloadData = bimServerClient.getDownloadData(downloadId, serializer .getOid());
	ByteArrayOutputStream baos = new ByteArrayOutputStream();
	IOUtils.copy(downloadData, baos);
	System.out.println(baos.size() + " bytes downloaded");

```
Examples on how to use the client-library can be found [here](https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/serviceinterface).

Examples on how to use the client-side EMF model can be found [here]( https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/emf)

Examples on how to use the low-level-calls from the client library are [here](https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/lowlevel)