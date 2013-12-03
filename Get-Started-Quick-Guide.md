**Note:** BIMserver is a platform for others to build applications on. We provide a stable and flexible platform to create online (open)BIM tools.

### **Stand-alone BIMserver**

1. Read [System Requirements for Ver 1.2](https://github.com/opensourceBIM/BIMserver/wiki/Requirements-1.2) or [Sytem Requirements for Ver 1.3](https://github.com/opensourceBIM/BIMserver/wiki/Requirements-1.3)

2. Make sure you can execute a JAR file by double-clicking a JAR file. If not, check that [Java](http://www.java.com) is installed properly and the JAVA environment variables are setup correctly.

3. Read about [which files to download](https://github.com/opensourceBIM/BIMserver/wiki/Download). Download the latest file, e.g. [bimserver-1.2.jar](http://bimserver.org/download/).
4. Read [JAR Starter](https://github.com/opensourceBIM/BIMserver/wiki/JAR-Starter). 
**Note**: After clicking the START button, it may take up to a few minutes for the BIMserver to load and configure various components. Wait until you see something like "INFO  org.bimserver.JarBimServer - Server started successfully" before clicking on "Launch Webbrowser".

5. Read [Setup Guide](https://github.com/opensourceBIM/BIMserver/wiki/Setup)
6. Watch this [Open Source BIMserver](http://www.youtube.com/watch?v=greB5jHi6JQ) video.

If the above steps are followed correctly, you should have BIMserver launched successfully on a browser with the URL and specified port number: http://localhost:8080. If failed, try again from Step 4 by specifying another port, e.g. instead of 8080, try 8082.

Once the BIMserver is launched successfully on the web browser, there may be a few more things to do  depending on which mode the BIMserver is in.

1. If the web page displays the status as "NOT SETUP", go to the admin page at http://localhost:[port]/admin, e.g. http://localhost:8080/admin
2. Complete the form and create your account as requested using your email address.
3. The current version of BIMserver has no user interface (GUI), so you need to use your own GUI to access BIMserver functionalities.
4. Each of the functionalities can be tested at http://localhost:[port]/console.html
5. There are also a number of resources available under specific sub-folders, e.g. http://locahost:[port]/js
6. BIMserver must remain running in the background for these functionalities to work via your own interface.

**Third party GUI:**

There are a few third party GUI available. Some are commercial products that you have to purchase a licence for, but there are a few that are free to try or shared freely by others. An open source example is http://test.bimvie.ws being developed by [Bimview.ws](http://www.bimvie.ws/).

**Note:** To use test.bimvie.ws, BIMserver must be running. Also, you need to specify the BIMserver's URL, i.e. http://localhost:8080 (or another port that you specified during setup).
