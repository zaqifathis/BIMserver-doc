How to install the BIMserver on a freshly installed Ubuntu 12.04.2 LTS Server

> These instructions are for the 1.2 release.

The machine this was tested on was a Ubuntu Server 12.04.2 LTS Amazon EC2 server (Ubuntu Cloud Guest AMI ID ami-d0f89fb9 (x86_64)) on an m1.xlarge machine.

# Introduction

This guide is used to install a BIMserver on a cloud based server. Root rights are assumed. When running as a normal user, prepend "sudo " to each command (or start your session with sudo -i).

Paths can be changed to your liking of course. This is just one way of doing things, yes you can use a different NTP server, yes you can use another JRE implementation etc...

Directories chosen for this installation:
```
/var/www/[YOUR DOMAIN]/ROOT.war // For the BIMserver WAR file
/opt/tomcat7 // For the Tomcat7 application
/var/bimserver/home // For the BIMserver home directory
```

# Commands

| Command | Description |
| ------------- | ------------- |
| apt-get update | Update the package index |
| apt-get upgrade | Upgrade installed packages |
| apt-get install openjdk-7-jre-headless wget unzip nano ntpdate | Install JRE 7 and some tools |
| ntpdate ntp2.xs4all.nl | Update the local time, useful when looking in log files |
| dpkg-reconfigure tzdata | Select timezone |
| mkdir /var/www | Create a /var/www directory if it's not already there |
| mkdir /var/www/(YOUR DOMAIN) | Create a directory for you domain |
| chown -R tomcat7 /var/www/(YOUR DOMAIN) | Give rights to tomcat7 user to write |
| mkdir /var/bimserver | Create a directory for you BIMserver home directory (this has nothing to do with /home on unix systems |
| chown -R tomcat7 /var/bimserver | Give the appropriate rights to the tomcat7 user |

```
nano /opt/tomcat7/conf/server.xml
```
Change the port attribute in the Connector tag to the desired port (please see: "Running op ports below 1024"
```
<Host name="[YOUR DOMAIN]" appBase="/var/www/[YOUR DOMAIN]" unpackWARs$
    <Context path="" docBase="/var/www/[YOUR DOMAIN]/ROOT.war">
        <Parameter name="homedir" value="/var/bimserver/home"/>
    </Context>
</Host>
```

Edit /etc/default/tomcat7 (with "nano" for example), change the line with "JAVA_OPTS" to: JAVA_OPTS="-Djava.awt.headless=true -Xmx12G -Xss4096k"

The 12G parameter indicates 12GB of heap memory, please adjust to your server (always keep a few hundred megabytes free for your OS and other apps).

Restart Tomcat: service tomcat7 restart

# Installing an STMP server

```
apt-get install postfix
```

Select "Internet server", use a real domain name that is pointing to your server's IP address.

# Running op ports below 1024

The tomcat7 user has no rights to bind to ports below 1024, to make the server available on port 80 (the default HTTP port), you can use iptables (you might have to install the package "iptables"):

```
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8080
```
to store these settings:
```
iptables-save
```