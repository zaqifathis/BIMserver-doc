When you are getting the "websocket error", this page helps you find the reason.

> Note, if you are using Tomcat 7, there is a special WAR build that uses an older API for supporting Web Sockets. For Tomcat 8 and other application containers you can use the normal WAR file (which uses JSR-356 for Web Sockets).

The webbased user interface that is currently being shipped with BIMserver is BIMvie.ws. BIMvie.ws requires a working WebSocket implementation in your browser. 
Usually when web sockets do not work, it's either one of the following: 
- You are on a corporate network and the system administrators do not allow you to use Web Sockets (either intentionally or not) 
- You are using a very old browser (usually Internet Explorer). Internet Explorer is not supported, but newer versions tend to work anyways.
- Your application container (Tomcat, Jetty or etc...) does not support web sockets, this should be in the log files.

The web socket technology has been standardized in 2011.