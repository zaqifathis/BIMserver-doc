# Starting points
- There are two roles, any application can provide just one of the roles, or both of them
  - A: Software that sends data to other software (B)
    Examples: CAD software (using e.g. IFC export), A BIMserver (after a user checks in)
  - B: Software that receives data from other software (A)
    Examples: Simulation software, BIMserver (simply storing the data, or running services).
- Other than in the previous version, in this version, it should be possible to issue all communication from A. The main advantage being that no listening sockets have to be opened on A. This is useful on corporate networks (or even private networks) and when A is for example CAD software.
- A service describes which input and which output formats it supports
- All communication will be JSON. For two methods (sending and receiving data), there will be alternative methods that perform better
- All authentication will be done with OAuth2

List of schemas has moved to: https://github.com/opensourceBIM/BIM-Bot-services/wiki/Schemas

- Setup OAuth
- Setup ServiceConfig
```java
long setData(String schema, byte[] data, String serviceConfigurationId);
Progress getProgress(long topicId);
byte[] getData(topicId);
ServiceDescriptor getServiceDescriptor(String serviceName);
```