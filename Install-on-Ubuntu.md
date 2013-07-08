> These instructions are for the 1.2 release.

How to install the BIMserver on a freshly installed Ubuntu 12.04.2 LTS Server Amazon EC2 server.

AMI: Ubuntu Cloud Guest AMI ID ami-d0f89fb9 (x86_64)
Instance: m1.xlarge machine

Of course most (if not all) of the instructions are generic enough for any Ubuntu installation.

# Introduction

This guide can be used to install a BIMserver on a cloud based server. Root rights are assumed. When running as a normal user, prepend "sudo " to each command (or start your session with sudo -i).

Paths can be changed to your liking of course. This is just one way of doing things, yes you can use a different NTP server, yes you can use another JRE implementation etc...

Directories chosen for this installation:
```
/var/www/[YOUR DOMAIN]/ROOT.war // For the BIMserver WAR file
/opt/tomcat7                    // For the Tomcat7 application
/var/bimserver/home             // For the BIMserver home directory
```

[YOUR DOMAIN] should be a DNS entry (can be a subdomain).

# Commands

## Basic configuration of Ubuntu
| Command | Description |
| ------------- | ------------- |
| apt-get update | Update the package index |
| apt-get upgrade | Upgrade installed packages |
| apt-get install openjdk-7-jre-headless wget unzip nano ntpdate | Install JRE 7 and some tools |
| ntpdate 0.nl.pool.ntp.org | Update the local time, useful when looking in log files |
| dpkg-reconfigure tzdata | Select timezone |

## Create directories / users
| Command | Description |
| ------------- | ------------- |
| mkdir /var/www | Create a /var/www directory if it's not already there |
| mkdir /var/www/[YOUR DOMAIN] | Create a directory for you domain |
| useradd -s /sbin/nologin tomcat7 | Create a tomcat7 user |
| chown -R tomcat7 /var/www/[YOUR DOMAIN] | Give rights to tomcat7 user to write |
| mkdir /var/bimserver | Create a directory for you BIMserver home directory (this has nothing to do with /home on unix systems |
| chown -R tomcat7 /var/bimserver | Give the appropriate rights to the tomcat7 user |

## Install Tomcat7
| Command | Description |
| ------------- | ------------- |
| cd /opt | Goto the /opt directory |
| wget http://apache.cs.uu.nl/dist/tomcat/tomcat-7/v7.0.41/bin/apache-tomcat-7.0.41.zip | Download tomcat (Make sure you replace this with the latest release!) |
| unzip apache-tomcat-7.0.41.zip | Unzip Tomcat7 |
| rm apache-tomcat-7.0.41.zip | Remove the downloaded zip file |
| mv apache-tomcat-7.0.41 tomcat7 | Rename to convenient name |
| chown -R tomcat7 /opt/tomcat7 | Change owner of directory tot tomcat7 |
| chmod +x /opt/tomcat7/bin/*.sh | Make .sh files executable |

Change the Tomcat7 configuration file:
```
nano /opt/tomcat7/conf/server.xml
```
Change the port attribute in the Connector tag to the desired port (also see: "Running op ports below 1024". Also add a new host, see below.
```
<Host name="[YOUR DOMAIN]" appBase="/var/www/[YOUR DOMAIN]" unpackWARs="true" autoDeploy="true" xmlValidation="false" xmlNamespaceAware="false">
    <Context path="" docBase="/var/www/[YOUR DOMAIN]/ROOT.war">
        <Parameter name="homedir" value="/var/bimserver/home"/>
    </Context>
</Host>
```

Edit /etc/default/tomcat7 (with "nano" for example), change the line with "JAVA_OPTS" to: JAVA_OPTS="-Djava.awt.headless=true -Xmx12G -Xss4096k"

The 12G parameter indicates 12GB of heap memory, please adjust to your server (always keep a few hundred megabytes free for your OS and other apps).

# Startup script

To be able to starts/stop/restart tomcat7 you need an init.d script. You can find one [https://gist.github.com/baylisscg/942150 here]. Copy this file to /etc/init.d/tomcat7 and give it execute permissions (chmod +x /etc/init.d/tomcat7).

Change the file:
'''
CATALINA_HOME=/opt/$NAME
CATALINA_BASE=/opt/$NAME
JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64/jre // Change this to your JRE directory
'''

Restart Tomcat: service tomcat7 restart

## Install BIMserver
| Command | Description |
| ------------- | ------------- |
| cd /var/www/[YOUR DOMAIN] | Go to your domain folder |
| wget http://code.google.com/p/bimserver/downloads/detail?name=bimserver-1.2.RC9-2013-06-25.war&can=2&q=&sort=uploaded+-filename -O ROOT.war | Download the latest BIMserver (Make sure you replace this with the latest version!) |

# Installing an STMP server

You only have to do this if you do not already have an accessible SMTP server running in your network or with your ISP. Remember running your own SMTP server is a security/spam risk if you don't know how to properly install/maintain it.

```
apt-get install postfix
```

Select "Internet server", use a real domain name that is pointing to your server's IP address.

# Running on ports below 1024

The tomcat7 user has no rights to bind to ports below 1024 (only root can), to make the server available on port 80 (the default HTTP port), you can use iptables (you might have to install the package "iptables"):

```
apt-get install iptables
iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j REDIRECT --to-port 8080
```
to store these settings:
```
iptables-save
```