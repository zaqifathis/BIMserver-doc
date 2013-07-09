# Introduction

Sometimes it is useful to embed the BIMserver in another application, this page describes how to do this.

Note: This way no webserver will be started so the web userinterface and SOAP/REST are not available.

# Details

1. Create a BIMserver instance
```java
BimServer bimServer = new BimServer(new File("home"), new LocalDevelopmentResourceFetcher());
```

2. Load plugins
```java
bimServer.getPluginManager().loadPluginsFromEclipseProject(new File("../CityGML"));
bimServer.getPluginManager().loadPluginsFromEclipseProject(new File("../Collada"));
bimServer.getPluginManager().loadPluginsFromEclipseProject(new File("../IfcPlugins"));
bimServer.getPluginManager().loadPluginsFromEclipseProject(new File("../MiscSerializers"));
bimServer.getPluginManager().loadPluginsFromEclipseProject(new File("../IfcEngine"));
bimServer.getPluginManager().loadPluginsFromEclipseProject(new File("../buildingSMARTLibrary"));
```

3. Start the server
```java
bimServer.start();
```

4. Use the BIMserver. All useful objects are available with getters on the BimServer object.
```java
BimDatabase bimDatabase = bimServer.getDatabase();
SettingsManager settingsManager = bimServer.getSettingsManager();
ServiceInterface systemService = bimServer.getSystemService();
EmfSerializerFactory emfSerializerFactory = bimServer.getEmfSerializerFactory();
DiskCacheManager diskCacheManager = bimServer.getDiskCacheManager();
VersionChecker versionChecker = bimServer.getVersionChecker();
ServiceFactory serviceFactory = bimServer.getServiceFactory();
ServerInfo serverInfo = bimServer.getServerInfo();
MailSystem mailSystem = bimServer.getMailSystem();
PluginManager pluginManager = bimServer.getPluginManager();
MergerFactory mergerFactory = bimServer.getMergerFactory();
LongActionManager longActionManager = bimServer.getLongActionManager();
```