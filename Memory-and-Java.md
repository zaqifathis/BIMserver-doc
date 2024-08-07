Since a lot of people ask questions about BIMserver and configuring it's Heap Size, this page hopes to clarify some details.

Java, unlike most native software, needs to know the maximum amount of memory it can use upfront. ou have to specify this maximum amount of memory (Heap Size) to the Java Virtual Machine (JVM) using the -Xmx argument. Here’s how to do it:

# Setting the Heap Size

## Examples:

For 4GB of memory:

```
-Xmx4g
```

For 16GB of memory:

```
-Xmx16g
```

# Important Considerations

## Memory Allocation:

- This amount of memory cannot be more than the physical (of virtual) memory of your machine. It has to be less then that because other software (including the OS) will also use memory. Depending on what OS/software is installed, keep at least 1GB free for the other software.
- Java will not necessarily use all the memory that is given, it is just a maximum amount it can use

## BIMserver Requirements:

- BIMserver needs at least 1GB
- Depending on usage and plugins, BIMserver might require up to 100GB.

## Operating System (OS) Limitations:

- 32-bit:

  - Maximum physical memory: 4GB.
  - 32-bit Java usually can use up to approximately 1300MB of memory, which is not much!

- 64-bit:
  - No strict limit as with 32-bit systems, allowing for more memory allocation.

## Java Version:

- Ensure you are using a 64-bit JVM on a 64-bit OS to avoid memory limitations.
- Using a 32-bit JVM on a 64-bit OS is not recommended and should be avoided.
