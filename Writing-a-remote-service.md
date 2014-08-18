1. Notifications are being send via HTTP, so the first thing you need is an HTTP server (this can be Apache for PHP, Jetty/Tomcat for Java etc...)
2. There should be 1 URL on which you will be receiving HTTP requests, for example: "http://myserver/json"
3. These requests will contain JSON messages encoded in UTF-8. The message format is the same as normal JSON messages that you use to access the BIMserver API (https://github.com/opensourceBIM/BIMserver/wiki/JSON-API).

# Register your service

After you have this running, register your service on a certain BIMserver project.

{{{

ServiceInterface.addServiceToProject(poid, sService);

The SService looks like this (in JSON):
			var service = {
				__type: "SService",
				name: $(".addservice2 .serviceName").val(),
				providerName: othis.serviceDescriptor.providerName,
				serviceIdentifier: othis.serviceDescriptor.identifier,
				serviceName: othis.serviceDescriptor.name,
				url: othis.serviceDescriptor.url,
				token: othis.token,
				notificationProtocol: othis.serviceDescriptor.notificationProtocol,
				description: othis.serviceDescriptor.description,
				trigger: othis.serviceDescriptor.trigger,
				profileIdentifier: profileDescriptor.identifier,
				profileName: profileDescriptor.name,
				profileDescription: profileDescriptor.description,
				profilePublic: profileDescriptor.publicProfile,
				readRevision: othis.serviceDescriptor.readRevision,
				readExtendedDataId: othis.readExtendedDataOid,
				writeRevisionId: othis.serviceDescriptor.writeRevision ? $(".addservice2 .projectSelect").val() : -1,
				writeExtendedDataId: othis.writeExtendedDataOid,
				modelCheckers: othis.modelCheckers
			};

}}}