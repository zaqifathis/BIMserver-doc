# Intro

To allow for more granular access to information stored in BIMserver, the "Low Level Calls" have been added. They are an alternative to the checkin/download calls.

# Workflow

## Start a transaction

First you call "startTransaction". The only parameter you have to give is the poid (ProjectID). This call will return a Transaction ID (tid). This Transaction ID will be used for all subsequent calls.

## Read/Write data

There are a lot of calls to read/write data. All of them can be found in the Bimsie1LowLevelInterfaceinterface. For example you can call 
```
getIntegerAttribute(tid, oid, "OverallWidth").
```

The oid is the ObjectID of the object of which you would like to get the attribute with the name "OverallWidth".

It's the same for changing attributes. For example you can call.
```
Bimsie1LowLevelInterface.setStringAttribute(tid, oid, "GlobalId", "GUID123455");
```