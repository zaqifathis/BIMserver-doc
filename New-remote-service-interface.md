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