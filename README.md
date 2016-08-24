# mitchallen/pi-cross-compile (Dockerfile)

A Dockerfile to allow cross-compiling C/C++ projects in Ubuntu that will run on a Raspberry Pi.

* * *

## Usage

Note that these instructions were written for a Mac.

To use this container you must pass it a local path that contains a __Makefile__ and a project to compile. In the example below, substitute __~/MY-PROJECTS/MY-BUILD__ with a path to your local project. Your folder must contain a valid make file called __Makefile__. The make file must contain references to the Raspberry Pi specific tools that will be described below.

    docker run -it -v ~/MY-PROJECTS/MY-BUILD:/build mitchallen/pi-cross-compile
    
* * *
    
### Example

If you had a root project folder called __~/raspberry__ and a child folder containing your make file and source code called __hello__ you would compile it for Raspberry Pi like this:

    docker run -it -v ~/raspberry/hello:/build mitchallen/pi-cross-compile
    
During the build process, output should be displayed in the terminal. On success, the container will exit and an executable that works on the Pi should be left in your local build directory.
   
* * *
 
## Tools

This image contains a call to download Raspberry Cross Compile tools that can be found here: [https://github.com/raspberrypi/tools.git](https://github.com/raspberrypi/tools.git). It places them in a folder called __pitools__.

The actual line is this:

    git clone --progress --verbose https://github.com/raspberrypi/tools.git --depth=1 pitools

To cross compile using __gcc__ for Raspberry Pi you would need a line like this in your Makefile:

    CC=/pitools/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin/arm-linux-gnueabihf-gcc

For other tools in that folder, browse [here](https://github.com/raspberrypi/tools/tree/master/arm-bcm2708/gcc-linaro-arm-linux-gnueabihf-raspbian-x64/bin).

* * *

## Running on Pi

Once your build is complete, the executable will not work on Ubuntu or a Mac. It will be up to you to copy it over to your Pi and test it.

* * *
 
## Repo(s)

* [bitbucket.org/mitchallen/pi-cross-compile.git](https://bitbucket.org/mitchallen/pi-cross-compile.git)
* [github.com/mitchallen/pi-cross-compile.git](https://github.com/mitchallen/pi-cross-compile.git)

* * *

## Contributing

In lieu of a formal style guide, take care to maintain the existing coding style.
Add unit tests for any new or changed functionality. Lint and test your code.

* * *

## Version History

#### Version 0.1.1 release notes

* Fixed type-o in README

#### Version 0.1.0 release notes

* Initial release

