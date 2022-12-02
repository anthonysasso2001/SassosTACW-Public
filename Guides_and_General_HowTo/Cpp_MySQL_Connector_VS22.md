# How to Enable the MySQL Connector for a Visual Studios [Enterprise, but Community would also work] C++ Project

Information Gathered from Various Sources, but major links are as follows:

1. [All MySQL Connectors guides & info, select C++ for this case](https://www.mysql.com/products/connector/).
2. [Dev guide for the connector](https://dev.mysql.com/doc/connector-cpp/8.0/en/connector-cpp-introduction.html).
3. [xDevAPI guides etc. as I prefer using this particular version than the others](https://dev.mysql.com/doc/x-devapi-userguide/en/).

---

## Pre-Linking, Download Steps
First we need to check if the connector exists & optionally download the debug version as well.

1. Go to *"C:\Program Files\MySQL\"* and check if there is a *"Connector C++ X"* folder [X is the version of your MySQL].
   1. If it is not installed get it from [this download link](https://dev.mysql.com/downloads/connector/cpp/), and I recommend choosing the "Windows (x86, 64-bit), MSI Installer".
2. In addition, you can download the "Windows (x86, 64-bit), ZIP Archive Debug Binaries" from the same site and put it into *"C:\Program Files\MySQL\"* after unzipping to become *"C:\Program Files\MySQL\mysql-connector-c++-8.0.28-winx64-debug\"*.

## Now these are the steps to link the connectors
[Note* Select the Apply option after each numbered step incase VS crashed or you close the window, assume all steps are in the *"Project > Properties"* tab unless otherwise stated].

1. Go to Project > Properties > C/C++ > General > Additional Include Directories and add:
   1. *"C:\Program Files\MySQL\Connector C++ 8.0\include"* for release.
   2. *"C:\Program Files\MySQL\mysql-connector-c++-8.0.28-winx64-debug\mysql-connector-c++-8.0.28-winx64\include"* for debug if downloaded.
   - You can also put different locations depending on the version, location etc that is being used in the program but these are the defaults for the *current* latest version of mysql I had.
   - (Make sure to use "" surrounding paths as there are spaces which can cause issues, otherwise use an ENV variable instead).
2. C/C++ > Preprocessor > Preprocessor Deinitions > *"STATIC_CONCPP"*.
3. C/C++ > Code Generation > Runtime Library > *"Multi-threaded DLL (/MD)"*.
4. Linker > General > Additional LIbrary Directories >
   1. *"C:\Program Files\MySQL\Connector C++ 8.0\lib64\vs14"* for release
   2. *"C:\Program Files\MySQL\mysql-connector-c++-8.0.28-winx64-debug\mysql-connector-c++-8.0.28-winx64\lib64\vs14\debug"* for debug if downloaded.
5. Linker > Input > Additional Dependencies > *"mycqlcppconn8-static.lib"* (swap the .lib name for earlier or later versions as needed).
6. Add all the necessary includes, this can be used for simplicity:
   1. *"#include <mysqlx/xdevapi.h>"*.