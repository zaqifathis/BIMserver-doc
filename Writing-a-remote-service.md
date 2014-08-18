1. Notifications are being send via HTTP, so the first thing you need is an HTTP server (this can be Apache for PHP, Jetty/Tomcat for Java etc...)
2. There should be 1 URL on which you will be receiving HTTP requests, for example: "http://myserver/json"
3. These requests will contain JSON messages encoded in UTF-8. The message format is the same as normal JSON messages that you use to access the BIMserver API (https://github.com/opensourceBIM/BIMserver/wiki/JSON-API).
4. Your service should at least respond to the following requests:

[Bimsie1RemoteServiceInterface.getService](https://github.com/opensourceBIM/BIMserver/blob/1.3/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1RemoteServiceInterface.java#L83)
[Bimsie1RemoteServiceInterface.getPublicProfiles](https://github.com/opensourceBIM/BIMserver/blob/1.3/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1RemoteServiceInterface.java#L74)
[Bimsie1RemoteServiceInterface.getPrivateProfiles](https://github.com/opensourceBIM/BIMserver/blob/1.3/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1RemoteServiceInterface.java#L78)

Optional:
[Bimsie1RemoteServiceInterface.newRevision](https://github.com/opensourceBIM/BIMserver/blob/1.3/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1RemoteServiceInterface.java#L41)
[Bimsie1RemoteServiceInterface.newExtendedDataOnProject](https://github.com/opensourceBIM/BIMserver/blob/1.3/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1RemoteServiceInterface.java#L52)
[Bimsie1RemoteServiceInterface.newExtendedDataOnRevision](https://github.com/opensourceBIM/BIMserver/blob/1.3/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1RemoteServiceInterface.java#L63)

# Register your service

After you have this running, register your service on a certain BIMserver project. You can use a graphical interface like BIMvie.ws for that, or use the API

First call
```

ServiceInterface.addServiceToProject(poid, sService);

The SService looks like this (in JSON):
	var service = {
		__type: "SService",
		name: "Name of your service",
		providerName: "Name of the provider",
		serviceIdentifier: "Service identifier",
		serviceName: "Name of the service",
		url: "URL of your service",
		token: "Token",
		notificationProtocol: "json",
		description: "description",
		trigger: othis.serviceDescriptor.trigger,
		profileIdentifier: "Identifier for the profile",
		profileName: "Name of the profile",
		profileDescription: "description of the profile",
		profilePublic: true|false,
		readRevision: othis.serviceDescriptor.readRevision,
		readExtendedDataId: othis.readExtendedDataOid,
		writeRevisionId: othis.serviceDescriptor.writeRevision ? $(".addservice2 .projectSelect").val() : -1,
				writeExtendedDataId: othis.writeExtendedDataOid,
				modelCheckers: othis.modelCheckers
			};

```