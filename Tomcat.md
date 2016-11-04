Although installing and configuring tomcat has been documented plenty on the web, this page will try and cover the main problems people have encountered when running BIMserver on tomcat.

# Version
To run BIMserver on Tomcat, you need version 8 or higher. 8.5 and 9 have both been tested and work.

# Tomcat on windows

Use the "32-bit/64-bit Windows Service Installer". This will install tomcat as a service. Installing it as a service makes it easier to configure for automatic start on boot.

## Setting the amount of heap memory

On windows, tomcat installs this little icon in your system tray ![](https://github.com/opensourceBIM/BIMserver/raw/master/Documentation/img/tomcaticon.png).
Right-Click on the icon and select "Configure...". The following window will appear:

![](https://github.com/opensourceBIM/BIMserver/raw/master/Documentation/img/tomcatconfigwindows.png)

Open the Java tab and you can change the max amount of memory. Make sure you restart tomcat after changing anything. Also make sure you check whether the max amount of memory is actually correct (by going to the Tomcat admin page, or by using BIMvie.ws)