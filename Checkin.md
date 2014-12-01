# Introduction

Checkin is the term used to upload complete models to a BIMserver. Because there are several ways to do it, and because it might not be very intuitive this page intends to clarify a few things.

# Usual way

The usual way would be to call the checkin method on the Bimsie1ServiceInterface. Just look at the documentation for the method. Skip to 

# Other way

Because of the overhead of the different implementations of the Service Interfaces, and because of the nature of the checkin method (pushing a lot of data) there is another way. You can (HTTP) POST the data to /upload. The required fields are:
```
token: The token you are using, this is the token you get from calling login
deserializerOid: Id of the deserializer you want to use
comment: A comment for this checkin
merge: Whether to merge or not (not working properly, just keep it to false)
poid: Id of the project
sync: Whether to call this synchronous or not
```

The upload servlet will return a bit of json, the structure:
```
{
  checkinid: The checkinid
}
```

If something goes wrong, it will return:
```
{
  exception: A message
}
```

# Using the checkinid

