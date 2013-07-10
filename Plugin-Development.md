# Introduction

The BIMserver project has a strong focus on interaction with other systems, that's what the (Service Interfaces)[Service Interfaces] are for (accessible via [SOAP](SOAP), [Protocol Buffers](Protocol Buffers) or [JSON](JSON-API)) but some logic will only work when running within the BIMserver, that's where plugins come into play.

# Types of plugins

All plugins implement the Plugin interface:
```java
public interface Plugin {
	void init(PluginManager pluginManager) throws PluginException; // Initialization code, if your plugin requires other plugins, this is the time to check for them, be sure to throw a PluginException when something is wrong
	String getName(); // A short name of this plugin
	String getDescription(); // A short description of this plugin
	String getVersion(); // A version, not used for dependencies (yet)
	boolean isInitialized(); // Should return whether this plugin is successfully initialized
}
```

Do not implement the Plugin class directly, there are sub-interfaces for the different purposes plugins can have.

# So how to develop a plugin

> This tutorial assumes you use eclipse, but other IDEs should also work

> The easiest way to learn is to look how other people have done things, there are quite a few plugins already, so have a look at them.

  * Create a new java project for your plugin, for example "PluginTest"
http://bimserver.googlecode.com/svn/wiki/images/newproject.png
  * Create your plugin class, this class must implement the plugin interface you want to write a plugin for, make sure you implement all methods correctly. For this example we will create a serializer and we will name the plugin "TestSerializerPlugin" in the package "test".
  * Create a plugin folder under your project
  * Create a plugin.xml file under the plugin folder, the content should like like this:
```xml
<?xml version="1.0" encoding="utf-8"?>
<PluginDescriptor>		
	<PluginImplementation>
		<interfaceClass>org.bimserver.plugins.serializers.SerializerPlugin</interfaceClass>
		<implementationClass>test.TestSerializerPlugin</implementationClass>
	</PluginImplementation>
</PluginDescriptor>
```

Now to test your plugin locally you will have to tell the BIMserver where your plugin can be found. Edit "LocalDevPluginLoader.java" and  look for the lines with loadPluginFromEclipseProject. Add

```java
pluginManager.loadPluginsFromEclipseProject(new File("../PluginTest"));
```

Now you can start the BIMserver and your plugin should be available as yet another way to serialize models.

To make your plugin available on deployed BIMservers (either WAR or JAR), you have to create a JAR file of your plugin. It should contain the compiled code, your plugin folder (+plugin.xml), and any required JAR files. The place of jar files doesn't matter, as long as they have the extension ".jar".

# License

The license under which the BIMserver.org software is released is a combination of Affero GPL, GPLv3 and/or LGPL (for binaries) from the GNU project. The different projects in our SVN repository are diffently licensed. More info on that can be found on our wiki.

Part of this license outlines requirements for derivative works, such as Plugins, GUI (themes), ObjectIDMs and (de)Serializers. Derivatives of BIMserver.org code inherit the Affero and/or GPL license.  There is some legal grey area regarding what is considered a derivative work, but we feel strongly that Plugins, Themes, ObjectIDMs and (de)Serializers are derivative work and thus inherit the Affero or GPL license. If you disagree, you might want to consider a different (open or closed source) project. We suggest some at http://osbim.org/projects/