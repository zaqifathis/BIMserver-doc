> Last updated for Eclipse Kepler

We use Eclipse to develop BIMserver. Other IDE's should work as well, but this page describes how to get started with Eclipse.

It's best to download the "Eclipse Modeling Tools" package, but if you are not going to change the EMF model, you can also just download the "Standard" package, or use your own existing installation.

# GitHub

All BIMserver project are on GitHub. Eclipse should have a Git client already.

* Copy the BIMserver GitHub URL to your clipboard (https://github.com/opensourceBIM/BIMserver.git)
* Open the GIT [perspective](http://stackoverflow.com/questions/6650353/just-what-is-an-eclipse-perspective-and-how-would-i-go-about-making-one) in Eclipse
* Right click in the "Git Repositories" view and select "Paste Repository Path or URI", or just press ctrl-v

![Add Repository](https://github.com/opensourceBIM/BIMserver/raw/master/Documentation/img/git1.png)

* Fill in your GitHub credentials if you have them.

![Credentials](https://github.com/opensourceBIM/BIMserver/raw/master/Documentation/img/git2.png)

* Next

![Credentials](https://github.com/opensourceBIM/BIMserver/raw/master/Documentation/img/git3.png)

* Finish (Select the "Import all existing projects after clone finishes" checkbox)

![Credentials](https://github.com/opensourceBIM/BIMserver/raw/master/Documentation/img/git4.png)

* Switch back to the Java perspective

# Running BIMserver from Eclipse

To run the BIMserver from eclipse, right click the BimServer project, select "Run As" and then "Java Application", eclipse will look for classes with main methods, you have to select "LocalDevBimServerStarter", which is in the package "org.bimserver".

## Not enough memory

When Java complains there is not enough memory, you can increase the amount of heap memory the BIMserver can use in the "Run configuration". Go to the tab "Arguments" and add the following to the "VM arguments": "-Xmx4g" (this is for 4GB of heap).

![Credentials](https://github.com/opensourceBIM/BIMserver/raw/master/Documentation/img/runconfigs.png)
![Credentials](https://github.com/opensourceBIM/BIMserver/raw/master/Documentation/img/runconfig.png)

>Make sure you are running a 64bit JVM when assigning more than 1300MB of heap!

# Setup

For local development, the BIMserver will be automatically setup. An administrator user with the username "admin@bimserver.org" will be created with the password "admin".

All of the API's are provided at http://localhost:8080, as well as a basic user interface. The admin interface is available at http://localhost:8080/admin.

You now have a working Eclipse environment, we look forward to your pull requests!