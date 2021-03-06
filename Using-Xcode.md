### Introduction
The project’s structure is quite complex and it’s not meant made to be debugged directly in XCode using the CMake Xcode Generator. Still, it’s possible to use the IDE to aid the development, it will allow to set up breakpoints, jump to definitions, and so on. 

### Steps

1) Configure the CMake project using the Makefile generator
> 
    mkdir -p builds/mk 
    cd builds/mk
    CMAKE_PREFIX_PATH=/usr/local/opt/qt5/ cmake ../../

(we will speak of a release build. add -DCMAKE_BUILD_TYPE=Debug if you want a Debug build)

2) Configure the CMake project using the Xcode Generator
> 
    mkdir -p builds/xcode
    cd builds/xcode
    CMAKE_PREFIX_PATH=/usr/local/opt/qt5/ cmake ../../ -G Xcode

3) Open the Xcode project, add a new Target, select Other -> External Build System
Fill the first fields with anything, like “obs xcode build” it doesn’t really matter. 
Build tool: /usr/bin/make
Click next, and select the Xcode directory that has been created before

4) A target will be created: in the External Tool Configuration, select the “mk” directory containing the Makefile

5) Select the New Target, build it (CMD-B). It will take a bit and won’t give any output. The target will be built in the folder mk/rundir/RelWithDebInfo/bin

6) In the Targets (Upper Left Corner), Edit Scheme -> Run -> Executable. Select the executable that has been placed in mk/rundir/RelWithDebInfo/bin/obs. Also check the “Use custom working directory” option in the Options pane and select your bin folder

7) Since the CMake output won’t be visible, and eventual build errors won’t be displayed properly, it makes sense to add the “obs” target as dependency for “obs xcode build”. This will double the compilation time but will display meaningful errors in Xcode

### Conclusion
That’s it! You can now set breakpoints, go to definitions and use all the features of the IDE
