This is just a proposal, lots of changes expected

September 2015
- Create roadmap
- Standardize on topicId, downloadId, laid, longActionId etc... and document
- Write more documentation
- Write a test that creates a 100GB database

Oktober 2015
- Convert to maven, publish on maven repository
- Load plugins on first use, to improve startup-time and memory consumption
- Maybe don't unpack JAR's on disk for plugins
- Setup a plugin repository (possibly using maven)
- Move non-essential plugins to different git repositories
- Deprecate code that will be removed
- Remove Bimsie1 namespace from all code (also update bimserverapi.js, BIMvie.ws, BIMsurfer etc...)

November 2015
- Remove query-plugin extensionpoint
- Implement indices for model-data
- Move GUID/Name indices to generic indexing system
- Implement useful query method, replace current query methods (https://github.com/opensourceBIM/BIMserver/wiki/New-query-langage)

December 2015
- Remove deprecated code (https://github.com/opensourceBIM/BIMserver/wiki/Deprecated)
- Add get/list/read methods to low level interface, remove data object calls
- Notifications on object-level
- Implement useful logging system (inc. notifications, log on disk)

January 2016
- Move usage of EMF model from server side to client side

Februari 2016
- Proof of concept scalable database implementation

Items to put on roadmap:
- Create HA ability (at least with 2 servers, 1 in standby)