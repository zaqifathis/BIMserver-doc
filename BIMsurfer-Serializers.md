For BIMsurfer 2 serializers are being used.

# SceneJsShellSerializer

This serializes the semantic information of the IFC model in JSON format. This contains no geometry. It's used by the sidebar showing the tree etc...

Example files:
* [Test 1 Shell.json](https://github.com/opensourceBIM/BIMserver/raw/dev/Documentation/files/Test 1 Shell.json)
* [Test 2 Shell.json](https://github.com/opensourceBIM/BIMserver/raw/dev/Documentation/files/Test 2 Shell.json)
* [Test 3 Shell.json](https://github.com/opensourceBIM/BIMserver/raw/dev/Documentation/files/Test 3 Shell.json)
* [Test 4 Shell.json](https://github.com/opensourceBIM/BIMserver/raw/dev/Documentation/files/Test 4 Shell.json)
* [Test 5 Shell.json](https://github.com/opensourceBIM/BIMserver/raw/dev/Documentation/files/Test 5 Shell.json)

# JsonGeometrySerializer

Serializes the geometry in JSON. Right now this serializer is being called for every (enabled and existing) IfcProduct subtype.

Example files:
* [Test 1.json](https://github.com/opensourceBIM/BIMserver/raw/dev/Documentation/files/Test 1.json)
* [Test 2.json](https://github.com/opensourceBIM/BIMserver/raw/dev/Documentation/files/Test 2.json)
* [Test 3.json](https://github.com/opensourceBIM/BIMserver/raw/dev/Documentation/files/Test 3.json)
* [Test 4.json](https://github.com/opensourceBIM/BIMserver/raw/dev/Documentation/files/Test 4.json)
* [Test 5.json](https://github.com/opensourceBIM/BIMserver/raw/dev/Documentation/files/Test 5.json)

# Older serializers

The older serializers "SceneJSSerializer" and "StreamingSceneJSSerializer" are not used anymore.