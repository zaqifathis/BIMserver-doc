Downloading models from a BIMserver can be done in different ways.

# Using JSON/SOAP/Protocol Buffers

This is the most consistent way, because all other communications with BIMserver happens in the same way.
The available methods are:
- ServiceInterface.downloadRevisions
- ServiceInterface.downloadByNewJsonQuery

# Using the download servlet (direct HTTP)

There are two reasons why this alternative method exists:
- To allow the models to be downloaded by browsers, in a way that the downloaded file does not have to be "extracted" from another file (for example JSON).
- For efficiency reasons (for example JSON would have to encode binary data in base64)