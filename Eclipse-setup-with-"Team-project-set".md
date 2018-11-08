"Team projects sets" is a feature  of Eclipse that allows you to quickly setup a large list of projects from multiple GIT repositories.

# Recipe

* Start with an empty workspace
* Go to File | Import | Team | Team Project Set
* Select the given file and import it, this can take a while

> Sometimes eclipse has a problem loading big projects. If you have a lot of compile/dependency problems right away, you can try the following two things:

* Project | Clean... (and then clear all projects), this will issue a complete recompile of everything
* Right Mouse on a project | Maven | Update Project ... | Select all projects => Ok

# Currently included repositories/projects

* All core BIMserver projects (BimServer, BimServerJar, BimServerWar etc...)
* BIMserver IfcOpenShell plugin
* IfcPlugins
* BinarySerializers
* BIMvie.ws
* BIMsurfer (v1)
* BIMserver JavaScript API