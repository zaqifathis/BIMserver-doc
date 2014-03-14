When connecting to BIMserver from another machine/process, you usually use the JSON, ProtocolBuffers or SOAP calls. Those are RPC-like calls that do or do not return something in a synchronous way.

Sometimes you want the communication to be issued the other way around. You want BIMserver to initiate. For this to work, the remote side has to tell the BIMserver it is interested.

# Step 1 - Register an endpoint

The remote side has to register an Endpoint. For now the only type of Endpoint available is a WebSocket. You have to setup a WebSocket to http://[YOUR HOST]:[OPTIONAL PORT]/[OPTIONAL CONTEXT]/stream. BIMserver will send a JSON message:
```
{
  welcome: 12345
}
```
You have to send your token next, this is the same token you use for normal calls to BIMserver
```
{
  token: ABCDE...
}
```
Then BIMserver will send you an EndpointID, this Endpoint will be matched with the User linked to the token yo sent earlier.
```
{
  endPointId: 12345...
}
```

Now you can use this EndpointID when registering for certain events, such as progress on some action:
``` 
Bimsie1NotificationRegistryInterface.registerProgressHandler(topicId, endPointId);
```

In the previos example the topicId is being returned by for example the Bimse1ServiceInterface.checkin method.