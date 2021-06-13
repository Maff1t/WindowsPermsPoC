## WindowsPermsPoC
A simple PoC to demonstrate that is possible to write Non writable memory and execute Non executable memory on Windows
You can build it using Visual Studio.

### Writing non-writable memory

This simple program, allocate a non-writable piece of memory using VirtualAlloc and writes a shellcode inside of it, using WriteVirtualMemory.

This is made possible by the fact that WriteVirtualMemory is a function designed for debuggers so, under the hood, it changes permissions and restores them at the end.

### Executing non-executable memory

At the end of our program, the permissions of the allocated memory is changed to READ_ONLY, and the shellcode is executed. How is this possible?

The execution of code in a non-executable memory area in modern operating systems is prevented by a protection system called DEP (Data Execution Prevention). However, this mechanism is not enforced by the operating system, but it is up to the developer decide whether to enable it or not in his program, e.g. by setting the [NXCOMPAT](https://docs.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2012/ms235442(v=vs.110)) flag in VisualStudio. More details about this, [here](https://medium.com/@simone.aonzo/the-importance-of-data-execution-prevention-in-malware-analysis-fd29d0c9e03e).
