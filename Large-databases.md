This page tries to explain why your database grows the way it does.

# Models

Obviously Building Information Models take up most of the space. BIMserver does versioning based on revisions. This means that every object will be stored with information about the project it belongs to, the revision it belongs to and it's own identifier.

When you are uploading multiple IFC files to the same project, all data will be stored. Even if only small parts of the model have changed, every object is stored again. The reason for this is that it's impossible for BIMserver to figure out what has changed, and which object have stayed the same.

That's why we also added the low level calls, to actually change models by telling what has changed, instead of telling what the new complete model looks like.

# Other data

Apart from the Building Information Models BIMserver also stores information about projects, revisions, users, checkouts, history etc... This data is also being versioned, but on a per-object basis. So if you change the name of a project, the project will be stored again in the database with a new revision number. Usually these objects don't take up too much space, but certain access patterns can definitely make this explode.