# cmake_project
This is how to make a default cmake project which can be used on any system.
Cmake is used to make the makefile of the project and then the make file is in turn used to actually build something hence the CMakeFiles.txt does not contain any build commands using gcc or g++.
The build files can go to a /out/build folder after cloning.
We also explore how to build a library together and also how to use github submodules which is one of the best ways to include a library from github to your C++ project.
To run the program run the following commands step by step : 
./configure.sh
./build.sh
./run.sh


to include the subModules : 
You can either use a git submodules init or something like that or just add certain code to cmake file 
