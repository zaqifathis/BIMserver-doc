The `Service Interfaces` are a set of defined interfaces for interaction with BIMserver. These interfaces are defined as (heavily annotated) Java interfaces.

All interfaces with the namespace `org.buildingsmart.bimsie1` are implementations of the [BIMsie standard](http://bimsie.openbimstandards.org/). All calls in the `org.bimserver` namespace are BIMserver specific calls.

# The interfaces

| Namespace | Name | Functionalities | Link |
| --------- | ---- | --------------- | ---- |
| org.bimserver | AdminInterface | | [AdminInterface.java](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/AdminInterface.java) |
| org.bimserver | AuthInterface | | [AuthInterface.java] (https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/AuthInterface.java)
| org.bimserver | MetaInterface | | [MetaInterface.java](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/MetaInterface.java)
| org.bimserver | PluginInterface | | [PluginInterface.java](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/PluginInterface.java)
| org.bimserver | ServiceInterface | | [ServiceInterface.java](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/ServiceInterface.java)
| org.bimserver | SettingsInterface | | [SettingsInterface.java](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/SettingsInterface.java)
| org.buildingsmart.bimsie1 | Bimsie1AuthInterface | | [Bimsie1AuthInterface.java](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1AuthInterface.java)
| org.buildingsmart.bimsie1 | Bimsie1LowLevelInterface | | [Bimsie1LowLevelInterface.java](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1LowLevelInterface.java)
| org.buildingsmart.bimsie1 | Bimsie1NotificationInterface | | [Bimsie1NotificationInterface](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1NotificationInterface.java)
| org.buildingsmart.bimsie1 | Bimsie1NotificationRegistryInterface | | [Bimsie1NotificationRegistryInterface](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1NotificationRegistryInterface.java)
| org.buildingsmart.bimsie1 | Bimsie1RemoteServiceInterface | | [Bimsie1RemoteServiceInterface.java](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1RemoteServiceInterface.java)
| org.buildingsmart.bimsie1 | Bimsie1ServiceInterface | | [Bimsie1ServiceInterface](https://github.com/opensourceBIM/BIMserver/blob/master/Shared/src/org/bimserver/shared/interfaces/bimsie1/Bimsie1ServiceInterface.java)

# Access

Access to these methods is provided through 3 different channels: [Protocol Buffers](Protocol Buffers), [SOAP](SOAP) and [JSON](JSON-API).