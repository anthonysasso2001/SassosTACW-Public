# How to create or link Projects/Libraries in a Visual Studios [Enterprise, but Community would also work] C++ Project

Information Gathered from Various Sources, but major links are as follows:
1. [StackOverflow's for linking already existing C++ static libraries](https://stackoverflow.com/a/23882710).
2. [Microsoft's info about linking and creating dynamic link libraries](https://learn.microsoft.com/en-us/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp).
3. [Official Boost getting started guide](https://www.boost.org/doc/libs/1_62_0/more/getting_started/windows.html).

## Notes and Considerations:
- Assume for most that you will be going to Project > Properties unless otherwise stated.
- Not for file path includes VS usually also lets you use relative paths such as *"..\folder"* and ENV variables.

---
## Link Projects/Libraries
### **C++ Source Linking**
1. C/C++ > General > Additional Include Directories > *"pathOfHeader\"*. if it is also a VS Project use *"$(SolutionDir)\nameOfIncludedProject\"*.
2. Linker > General > *"pathOfObjFiles"* or *"$(SolutionDir)\nameOfIncludedProject\$(IntDir)\"*.
3. Linker > Input > Additional Dependencies > *"nameOfIncludedObj.obj"* or *"\*.obj"* to include all from that project.
4. In a file from the project use *[#include "nameof.h/hpp"]*.

### **C++ Library Linking**
#### Pre-existing Static & Dynamic Libraries
1. C/C++ > General > Additional Include Directories > *"pathOfLibHeader\"*. To tell the program the [.h or .hpp] containing folder.
2. Linker > General > Additional Library Directories > *"pathToLib\"*. This is also required for dll as there will be a .lib associated with it.
3. Linker > Input > Additional Dependencies >[*"nameOf.lib"* or *"\*.lib"*]. Needed for including all libraries in all linked files, but this is not recommended as it can introduce unknown dependencies without that much convenience.
4. If there are still issues with the **dll** option, then MS suggests adding the .dll to the folder manually in a post build event using the below code, which will increase the likelihood the program will be able to find the needed .dll.
   - Configuration Properties > Build Events > Post-Build Event > Command Line > *[xcopy \y \d "pathToFile\nameOf.dll" "$(OutDir)"]*.

---
## Common Third-Party Libraries and includes
### **Boost Library Linking**
1. Download Boost from [this website] navigating to the Windows x64 version, and ideally putting it into a created *"C:\Program Files\boost\extractedBoostVersionFolder"* directory or similar.
   - Based off the Boost suggestion for how to set this up, can put it anywhere as long as you link it correctly.
2. Use *"#include <boost/boostInclude.hpp>"* but may need to swap <> with "" depending on the lib in question.
3. Link the files using the following steps (essentially a copy of the static and dynamic lib linking):
    1. Config Properties > C/C++ > General > Additional Include Directories > *"C:\PathToBoostVersion"*.
    2. C/C++ > Precompiled Headers > change to **NOT** using precompiled headers if on yes.
    3. Build Solution. 
- Some can be build from source, this can be done with *"bootstrap" ".\b2"* in the boost version root directory.

### **MPI Linking**
1. Download some MPI library for Cpp (official ones are depreciated but there are a few options), I recommend MicrosoftMPI as it seems fine and definately works on VS22 [official download link](https://learn.microsoft.com/en-us/message-passing-interface/microsoft-mpi#ms-mpi-downloads) I also suggest using the msi installer to guarentee it is in the right place.
2. C/C++ > Additional Include Directories > *"C:\Program Files %28x86%29\Microsoft SDKs\MPI\Include"*.
3. Linker > General > *"C:\Program Files %28x86%29\Microsoft SDKs\MPI\Lib\x64"* or use x86 for 32 bit.
4. Linker > Input > *"msmpi.lib"*.

### **Enabling OpenMP**
1. Go to Properties > C/C++ > Language > OpenMP Support > Change to Yes.