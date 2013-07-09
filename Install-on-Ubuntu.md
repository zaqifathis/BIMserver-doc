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
| chmod +x /opt/tomcat7/bin/*.sh | Make .sh files executable |
| mkdir /opt/tomcat7/conf/policy.d | Create a policy directory |
| nano /opt/tomcat7/conf/policy.d/default.policy | Edit the default policy file |

Paste the following default code (you can change this later!)
```
grant {
  permission java.security.AllPermission;
};
```

| Command | Description |
| ------------- | ------------- |
| chown -R tomcat7 /opt/tomcat7 | Change owner of directory tot tomcat7 |

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

# Startup script

To be able to starts/stop/restart tomcat7 you need an init.d script. You can find one [https://gist.github.com/baylisscg/942150 here]. Copy this file to /etc/init.d/tomcat7 and give it execute permissions (`chmod +x /etc/init.d/tomcat7`).

Change the file:
```bash
CATALINA_HOME=/opt/$NAME
CATALINA_BASE=/opt/$NAME
TOMCAT7_SECURITY=no // You can change this to yes later on
JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64/jre // Change this to your JRE directory
```

Find the line that says:
```bash
JAVA_OPTS="-Djava.awt.headless=true -Xmx4G"
```
and change the amount of heap memory to your liking. Always keep a few hundred megabytes free for your OS and other applications.

Restart Tomcat: `service tomcat7 restart`

## Install BIMserver
| Command | Description |
| ------------- | ------------- |
| cd /var/www/[YOUR DOMAIN] | Go to your domain folder |
| wget https://bimserver.googlecode.com/files/bimserver-1.2.war -O ROOT.war | Download the latest BIMserver (Make sure you replace this with the latest version!) |

After this command, Tomcat 7 should start unpacking the downloaded war file in a directory called ROOT. After a while you should be able to connect to the BIMserver with a browser on your http://[YOUR DOMAIN]:[CONFIGURED PORT]. The page you will see should be showing the version of BIMserver and the status (should be NOT_SETUP if this is your first install). Continue to [Setup][setup] for further configuration.

When things are not working, you can look in the Tomcat 7 log file: /opt/tomcat7/logs/catalina.out and the BIMserver log file: /var/bimserver/home/logs/bimserver.log.

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

> If you are running on Amazon or another Cloud provider, make sure you enable port 80 (or whatever port you redirect) on their firewall as well.