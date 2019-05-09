# buildfile2cmake

Creates CMake project files from SCRAM BuildFile.xml files.

## Usage

`cd` into a directory containing a SCRAM BuildFile.xml files.
Then run `PATH/TO/REPO/buildfile2cmake.py`. Done!

The included builtin.json uses cmake variables defined by the cmake modlues in https://github.com/hsf/cmaketools as well as standard CMake modules.

Original script scram2cmake.py originated here
https://github.com/Teemperor/scram2cmake
