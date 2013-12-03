A few notes about memory usage

# Introduction

The BIMserver uses quite some memory, this page will explain how it's used.

# BerkeleyDB Cache

BerkeleyDB (the database engine the BIMserver uses) has a setting for the amount of heap memory it can use for caching (which will speedup reads), we have set it to 25%. So if you give your BIMserver 4GB of heap, it will soon be using 1GB of memory for caching. You can change this and other parameters only if you build [your own version of BIMserver](https://github.com/opensourceBIM/BIMserver)

See [http://docs.oracle.com/cd/E17277_02/html/java/com/sleepycat/je/EnvironmentMutableConfig.html#setCachePercent(int) the BerkeleyDB documentation] for more information

# Compressed Oops

Running a 64bit system with less than 32GB of memory, you can use [http://docs.oracle.com/javase/7/docs/technotes/guides/vm/performance-enhancements-7.html#compressedOop Compressed Ooops]. 

> Update: This is by default enabled on recent OpenJDK 6 and 7 implementations, so you probably won't have to do anything.