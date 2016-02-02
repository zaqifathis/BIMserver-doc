For the BIMserver 1.5 release, plugins have changed quite a bit.

For starters they depend on maven now. In the long term the plan is to also support non-maven plugins, but for now it's a requirement. To make the transition for older plugins easier, and to help developers of new plugins, this document describes how it works.

BIMserver specific terminology:
- Plugin: A plugin (implementing org.bimserver.plugins.Plugin)
- PluginBundle: A collections of 1 or more plugins, for example the org.opensourcebim.ifcplugins bundle has 18 plugins.

# Create a maven project

Most Java IDEs should support this. The pom file should have:

```<groupId>org.opensourcebim</groupId>```
For most plugins for bimserver this is org.opensourcebim, but this can be anything of course, make sure to use lowercase, which is the convention

```<artifactId>ifcplugins</artifactId>```
This should describe your plugin bundle, also make sure it is lowercase

```<version>0.0.8-SNAPSHOT</version>```
Make sure your version on SCM always ends in -SNAPSHOT and releases always omit -SNAPSHOT

```
<properties>
	<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```


## 