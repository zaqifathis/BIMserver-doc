[This](https://github.com/opensourceBIM/BIMserver/wiki/Service-Plugin) page has a description how to write internal services, but as most internal services seem to either checkin an updated revision, or add extended data, some convenience classes have been written that make it a lot easier to write an internal service. This page describes how to use those classes.

# A service that adds extended data

These services are triggered by a new revision, and add extended data to the revision.

First subclass "AbstractAddExtendedDataService", which can be found in the package "org.bimserver.plugins.services" in the "Shared" project.

Then you need to create a constructor and implement 2 methods:
- [newRevision](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/plugins/services/AbstractService.java#L92)
- [getProgressType](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/plugins/services/AbstractService.java#L98)

Full code:

```
package org.bimserver.demoplugins.service;

import org.apache.commons.io.IOUtils;
import org.bimserver.interfaces.objects.SObjectType;
import org.bimserver.plugins.services.AbstractAddExtendedDataService;
import org.bimserver.plugins.services.BimServerClientInterface;

public class HtmlService extends AbstractAddExtendedDataService {
        // A unique namespace, this is used by other software to determine the type of file you uploaded as extended data
	private static final String NAMESPACE = "htmldemo";

        // Constructor
	public HtmlService() {
                // Give a sensible name and description for the service
		super("HTML Demo Service", "HTML Demo Service");
	}

        // This is the method that gets called when there is a new revision, have a look at the [documentation](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/plugins/services/AbstractService.java#L92) for the details
	@Override
	public void newRevision(RunningService runningService, BimServerClientInterface bimServerClientInterface, long poid, long roid, String userToken, long soid, SObjectType settings) throws Exception {
		byte[] bytes = IOUtils.toByteArray(getPluginContext().getResourceAsInputStream("data/example.html"));
		addExtendedData(bytes, "example.html", "HTML Demo Results", "text/html", bimServerClientInterface, roid, NAMESPACE);
	}

        // Method to let BIMserver know whether you are going to provide progress-data
	@Override
	public ProgressType getProgressType() {
		return ProgressType.UNKNOWN;
	}
}
```