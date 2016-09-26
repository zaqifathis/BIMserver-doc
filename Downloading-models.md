Downloading models from a BIMserver can be done in different ways.

# Using JSON/SOAP/Protocol Buffers

This is the most consistent way, because all other communications with BIMserver happens in the same way. The are 2 methods available. Both methods return a TopicId. This TopicId can be passed to ServiceInterface.getDownloadData to get the actual data.

## ServiceInterface.downloadRevisions
This will just download 1 or more revisions.

## ServiceInterface.downloadByNewJsonQuery
This method allows you to do some filtering by supplying a query.

# Using the download servlet (direct HTTP)

There are two reasons why this alternative method exists:
- To allow the models to be downloaded by browsers, in a way that the downloaded file does not have to be "extracted" from another file (for example JSON).
- For efficiency reasons (for example JSON would have to encode binary data in base64)

The way to use this method is to send a HTTP GET to [yourbimserver]/download. The required parameters:
| Name | Description | Required |
|---|---|---|
| token | Your BIMserver auth token | Yes |
| topicId | The TopicId returned by either downloadRevisions or downloadByNewJsonQuery | Yes |
| serializerOid | The serializer you want to use | Yes |
| zip | Whether to download the content in a ZIP file | No |
