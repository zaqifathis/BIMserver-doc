# Starting points
- There are two roles, any application can provide just one of the roles, or both of them
  - Software that sends data to other software
  - Software that receives data from other software
- Other than the previous version, in this version, it should be possible to issue all communication from A, the main advantage being that no listening sockets have to be opened on A. This is useful on corporate networks (or even private networks) and when A is for example CAD software.

# List of schemas
- Ifc2x3tc1
- Ifc4
- BCF1.0
- BCF2.0

# List of formats
- Step
- Xml

- Setup OAuth
- Setup ServiceConfig
```java
long setData(String schema, byte[] data, String serviceConfigurationId);
Progress getProgress(long topicId);
byte[] getData(topicId);
ServiceDescriptor getServiceDescriptor(String serviceName);
```