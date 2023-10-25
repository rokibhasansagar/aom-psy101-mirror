README.md
=========
# another aom psy fork

Contains selected patches from https://github.com/BlueSwordM/aom-av1-psy/tree/Endless_Possibility and
its fork https://github.com/Clybius/aom-av1-lavish/tree/Endless_Instability, as well as original changes.


## Building the library and applications

### Prerequisites

 1. [CMake](https://cmake.org). See CMakeLists.txt for the minimum version
    required.
 2. [Git](https://git-scm.com/).
 3. [Perl](https://www.perl.org/).
 4. For x86 targets, [yasm](http://yasm.tortall.net/), which is preferred, or a
    recent version of [nasm](http://www.nasm.us/). If you download yasm with
    the intention to work with Visual Studio, please download win32.exe or
    win64.exe and rename it into yasm.exe. DO NOT download or use vsyasm.exe.
 5. Building the documentation requires
   [doxygen version 1.8.10 or newer](http://doxygen.org).
 6. Emscripten builds require the portable
   [EMSDK](https://kripken.github.io/emscripten-site/index.html).

### Get the code

~~~
    $ git clone https://gitlab.com/damian101/aom.git -b psy101 aom-psy101/
    $ cd aom-psy101/
~~~


### Basic build

CMake replaces the configure step typical of many projects. Running CMake will
produce configuration and build files for the currently selected CMake
generator. For most systems the default generator is Unix Makefiles. The basic
form of a makefile build is the following:

~~~
    $ cmake path/to/aom-psy101
    $ make
~~~

The above will generate a makefile build that produces the AV1 library and
applications for the current host system after the make step completes
successfully. The compiler chosen varies by host platform, but a general rule
applies: On systems where cc and c++ are present in $PATH at the time CMake is
run the generated build will use cc and c++ by default.


### Configuration options

The AV1 codec library has a great many configuration options. These come in two
varieties:

 1. Build system configuration options. These have the form `ENABLE_FEATURE`.
 2. AV1 codec configuration options. These have the form `CONFIG_FEATURE`.

Both types of options are set at the time CMake is run. The following example
enables ccache, disables unit tests and disables the AV1 decoder:

~~~
    $ cmake path/to/aom -DENABLE_CCACHE=1 -DENABLE_TESTS=0 -DCONFIG_AV1_DECODER=0
    $ make
~~~

The available configuration options are too numerous to list here. Build system
configuration options can be found at the top of the CMakeLists.txt file found
in the root of the AV1 repository, and AV1 codec configuration options can
currently be found in the file `build/cmake/aom_config_defaults.cmake`.


### Build with VMAF support

After installing
[libvmaf.a](https://github.com/Netflix/vmaf/tree/master/libvmaf),
you can use it with the encoder:

~~~
    $ cmake path/to/aom-psy101 -DCONFIG_TUNE_VMAF=1
~~~

Please note that the default VMAF model
("/usr/local/share/model/vmaf_v0.6.1.json")
will be used unless you set the following flag when running the encoder:

~~~
    # --vmaf-model-path=path/to/model
~~~


### Concrete building and installation example, for Linux

~~~
    $ git clone https://gitlab.com/damian101/aom.git -b psy101 aom-psy101/ && cd aom-psy101/
    $ mkdir aom_build && cd aom_build
    $ cmake .. -DENABLE_TESTS=0 -DCONFIG_AV1_DECODER=0 -DENABLE_DOCS=0 -DCONFIG_TUNE_VMAF=1 -DCMAKE_CXX_FLAGS="-flto -O3 -march=native" -DCMAKE_C_FLAGS="-flto -O3 -march=native" && make -j 16
    $ sudo cp aomenc /usr/bin/
~~~


## Support

This library is an open source project supported by the general AV1 enthusiast encoder community. Please send pull requests, feature requests and general comments on this repository.
Other more miscalleneous discussions, contributions, and talks will be done elsewhere.


## Bug reports

Bug reports can be filed in the Alliance for Open Media for general aomenc bugs
[issue tracker](https://bugs.chromium.org/p/aomedia/issues/list).

As for the ones related to this fork itself, the issues tab can be used here on GitLab.
