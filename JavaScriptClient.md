To make communication with the BIMserver easier we have made a simple API library you can use. Of course you can also implement your own API in JavaScript.

# Requirements

The API is just one file: bimserverapi.js. You can find it on http://[addressofyourserver]:[port]/[optional context path]/js/bimserverapi.js. You can copy it to your own project, but make sure you update the file when you update your BIMserver. There are a few dependencies, which are also on the BIMserver: "sha256.js" for encryption, "String.js" for some additional String manipulation functions, "jquery.cookie.js" for cookie functionality and   "jquery-2.0.2.min.js" as well. For some browsers not supporting "forEach" on arrays you might also need "array.js".

# Communication

The JavaScript API will communicate via JSON for most of the functions. Only downloading and uploading will sometimes be done without using JSON for performance reasons.

# Bootstrapping

Here is a little code snippet to bootstrap loading a BimServerApi. The notifier object should have the "error" method. The callback will be called on success.
```javascript
function loadBimServerApi(address, notifier, callback) {
	var timeoutId = window.setTimeout(function() {
		notifier.error("Could not connect");
	}, 3000);
	$.getScript(address + "/js/bimserverapi.js").done(function(){
		window.clearTimeout(timeoutId);
		Global.bimServerApi = new BimServerApi(address, notifier);
		Global.bimServerApi.init(function(){
			Global.bimServerApi.call("ServiceInterface", "getServerInfo", {}, function(serverInfo){
				callback(serverInfo);
			});
		});
	}).fail(function(jqxhr, settings, exception){
		window.clearTimeout(timeoutId);
		notifier.error("Could not connect");
	});
}
```

When you use the above snippet, you will get a "serverInfo" object back in the callback, this will indicate the state of the running BIMserver:
```javascript
	if (serverInfo.serverState == "NOT_SETUP") {
		// The server has not yet been setup, maybe your GUI can provide a way of doing this
	} else if (serverInfo.serverState == "UNDEFINED") {
		// This should never happen...
	} else if (serverInfo.serverState == "MIGRATION_REQUIRED") {
		// Migration is required before the BIMserver can function again, maybe you GUI can provide a way of doing this
	} else if (serverInfo.serverState == "MIGRATION_IMPOSSIBLE") {
		// There is no migration possible from the current database to the BIMserver version you are using, remove your database, or rollback to a previous version of BIMserver
	} else if (serverInfo.serverState == "FATAL_ERROR") {
		// Something fatal has occured, usually this has to do with limited resources such as memory or harddisk space
	} else if (serverInfo.serverState == "RUNNING") {
		var username = $("#inputEmail").val()
		Global.bimServerApi.login(username, $("#inputPassword").val(), $("#rememberMe").is(":checked"), function(data){
			// Success, we can nog login if we want
		});
	}
```

# Using the API

All methods in the [Service Interfaces](Service-Interfaces) can be called (make sure you look at the right documentation for your version). You must always use all parameters that are defined. Also when sending complex objects, you should define all the properties of the objects. The first call you will usually do is to login.

```javascript
	bimServerApi.login(username, password, rememberme, function(data){
		// Success
	});
```

Not all calls have been implemented in the JavaScript API, but it is very easy to use them anyways. The following example will list all the available projects:

```javascript
	bimServerApi.call("Bimsie1ServiceInterface", "getAllProjects", {onlyTopLevel: true, onlyActive: true}, function(data){
		data.forEach(function(project){
			console.log(project);
		});
	});
```

> TODO: Document the use of the Model class