Downloading models from a BIMserver can be done in different ways.

# Using JSON/SOAP/Protocol Buffers

This is the most consistent way, because all other communications with BIMserver happens in the same way. The method you call is "ServiceInterface.download". This method returns a TopicId (Long). This TopicId can be passed to ServiceInterface.getDownloadData to get the actual data. This process has been splitted over 2 methods because the process potentially takes a long time and could produce errors along the way. The TopicId can also be used to get information about the progress.

# Using the download servlet (direct HTTP)

There are two reasons why this alternative method exists:
- To allow the models to be downloaded by browsers, in a way that the downloaded file does not have to be "extracted" from another file (for example JSON).
- For efficiency reasons (for example JSON would have to encode binary data in base64)

The way to use this method is to send a HTTP GET to [yourbimserver]/download. The required parameters:

| Name | Description | Required |
|---|---|---|
| token | Your BIMserver auth token | Yes |
| topicId | The TopicId returned by either the download method | Yes |
| serializerOid | The serializer you want to use | Yes |
| zip | Whether to download the content in a ZIP file. Even if this argument is not "on" or not supplied, the content might still be compressed, this depends on the HTTP headers sent/received | No |
