> Work in progress

Definition:
A: Server that will be sending the notifications, usually triggered by a new revision
B: Server that will be receiving the notifications (and returns data)

To find services that are available, A can use https://github.com/opensourceBIM/BIMserver-Repository/blob/master/servicesnew.json.

# JSON format
This JSON describes the services available. At the moment there can be only one repository setup in a BIMserver, in the future you'll be able to store more repository addresses.

Example of one single entry (the actual json would be an array of these objects)
```json
"services": [
    {
      "name": "Fake clashdetection service",
      "description": "Fake clashdetection service",
      "provider": "Provider",
      "inputs": ["IFC_JSON_2x3TC1", "IFC_JSON_4"],
      "outputs": ["BCF_ZIP_1_0", "BCF_ZIP_2_0"],
      "resourceUrl": "https://test.logic-labs.nl/services/clashdetection.php",
      "authorizationUrl": "https://test.logic-labs.nl/authorize.php",
      "registerUrl": "https://test.logic-labs.nl/register.php",
      "tokenUrl": "https://test.logic-labs.nl/token.php" 
    }
```

The inputs array describes the input types this service is able to handle. The outputs array describes which output formats it is able output. Tje registerUrl, authorizationUrl, tokenUrl and resourceUrl are used for OAuth (described later in this document).

1. Register application

Oauth requires to register applications first. "A" will send an OAuth registration request to the registration endpoint of B (this is the "registerUrl" field of the JSON configuration). When implementing A, it can be useful to try and use an OAuth library. The registration JSON looks like this:

```json
{
  "type": "no idea what it's for",
  "client_name": "Name of the client",
  "client_url": "URL of client",
  "client_description": "Description of client",
  "client_icon": "",
  "redirect_url": ""
}
```

The response should look something like this:
```json
{
  client_id: 
  client_secret:
  issued_at:
  expires_in:
}
```

B will come up with a client_id (usually based on client_name) and client_secret. This is basically a shared secret. B should store this information. A should store this information as well because it is used in further communication.

The above process is only needed once per server-server link.

2. Authorization

This happens when a user of A adds a service. A will create a forward URL based on the "authorizationUrl" and client_id/secret generated in the previous step. The browser is then forwarded to this URL. B will have to handle this request. Depending on factors like available cookies/session and other settings, B can show multiple pages to the user asking for login credentials and/or the user's consent to allow A to send data to B. The last step in this process is to redirect the user back to A.

In this case no JSON is used, but URL parameters are, no clue why, that's just how OAuth works.

Fields in the URL:
client_id, response_type, state. B can use the client_id to match with the database.

In the final URL to which the user is forwarded, B should include a "code". A will use this code combined with the client_secret to get a token from B.

3. Getting a token
A will send a JSON to B:
```json
{
  grant_type:
  code:
  client_id,
  client_secret
}
```

B responds with:
```json
{
  access_token: access_token
}
```

A should store this access_token. The authentication is now successfull and A will be allowed to authenticate on B on the user's behalve.

4. Using resource
At a certain point, A will trigger B. This can be triggered manually by a user, or automatically as a response to a newly uploaded revision for example. A will send a HTTP POST request to B ("resourceUrl" in the JSON). This POST request should have a HTTP header:
```
Authorization: Bearer [access_token]
```

This header tells B that A will be authorized as user X.
The request body should contain the data A wants to send to B. The format of this data can be anything, but it should be negotiated earlier. B will keep the HTTP request open until it is reading processing the data. B will then put the resulting data in the POST response body. A will then usually store this data (as extended data on BIMserver).

Extra HTTP response header fields that will be processed when available:
```
Content-Disposition (for example 'attachment; filename="[filename]"')
Content-Type (for example: "application/json")
```