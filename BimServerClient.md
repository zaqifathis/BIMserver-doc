To connect to a BIMserver you can use one of the 3 protocols: [SOAP](SOAP), [JSON](JSON) or [Protocol Buffers](Protocol---Buffers). To make connecting to a BIMserver even easier, there also is a Java library you can use.

# Get the client library

You can download a nightly build [here](http://tools.bimtoolset.org/BIMserver/nightly%20builds/), select the latest date, and then the file named "bimserver-client-lib-[date].zip".

Extract the zipfile, copy the jar files from the "lib" and "dep" folders to your own project and include them in the build path.

Of course you can also use the client from source code, in that case download a source zip file, or checkout the projects from GIT.

# Example
Connecting via SOAP with authentication, and listing all projects

```java
	// Create a BimServerClientFactory, change Json to ProtocolBuffers or Soap if you like
	BimServerClientFactory factory = new JsonBimServerClientFactory("http://localhost:8080");
			
	// Create a new BimServerClient with authentication
	BimServerClient bimServerClient = factory.create(new UsernamePasswordAuthenticationInfo("admin@bimserver.org", "admin"));

        // List project names
	for (SProject project : bimServerClient .getBimsie1ServiceInterface().getAllProjects(true, true)) {
		System.out.println(project.getName());
	}

```

Examples on how to use the client-library can be found [here](https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/serviceinterface).

Examples on how to use the client-side EMF model can be found [here]( https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/emf)

Examples on how to use the low-level-calls from the client library are [here](https://github.com/opensourceBIM/BIMserver/tree/master/Tests/test/org/bimserver/tests/lowlevel)