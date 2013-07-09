#summary Eclipse Modeling Framework.

= Introduction =

Building Information Models (BIM) are typically Object Oriented and tend to be large. For example the Industry Foundations Classes (IFC) have more than one thousand different classes. Because the BIMserver has been written in Java (an Object Oriented Language), it is very useful to have typed Java classes in the used BIM model. This is where the [http://www.eclipse.org/modeling/emf/ Eclipse Modeling Framework (EMF)] comes into play. For now, the BIMserver uses IFC2x3tc1 internally.

= IFC Schema =

Most BIM meta models are described in a data format. As IFC is based on [http://en.wikipedia.org/wiki/EXPRESS_(data_modeling_language) STEP/EXPRESS] technology, the schema is available as an .EXP file. This file has been converted to an [http://download.eclipse.org/modeling/emf/emf/javadoc/2.6.0/org/eclipse/emf/ecore/package-summary.html#details EMF ECore] file with the [https://bimserver.googlecode.com/svn/branches/1.0/buildingSMARTLibrary BuildingSMARTLibrary] (part of BIMserver project).

= Generating Code =

The EMF framework generates Java classes with the given ECore file, these classes are used to store BIM models and passed to the [Database_internals database layer].

= Caveats =

If you load a model from an IFC-Step file, the String values of floating point numbers are being stored as a String as well. If you change the float values programatically, you should update (or clear) the string value.

= Three models =

BIMserver consists of 3 different EMF models:
 # the IFC Schema model (as described above) that holds IFC data.
 # the Log schema for logging
 # the 'store' model that  holds typical BIMserver data like projects, users, revisions etc. More info about this can be found on the [StoreModel] wiki page