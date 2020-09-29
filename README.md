# buildfile2cmake

Creates CMake project files from SCRAM BuildFile.xml files.

## Usage

`cd` into a directory containing a SCRAM BuildFile.xml files.
Then run `PATH/TO/REPO/buildfile2cmake`.

The included builtin.json uses cmake variables defined by the cmake modlues in https://github.com/hsf/cmaketools as well as standard CMake modules.

Original script scram2cmake.py originated here
https://github.com/Teemperor/scram2cmake


The dictionaries branch has been tailored to only build the CMSSW ROOT dictionary libraries.
To use.

# Set up a scram project area

scram pro CMSSW CMSSW_11_2_0_pre6

# Checkout all CMSSW packages

cd CMSSW_11_2_0_pre6/src
eval `scram runtime -sh`
git-cms-add-pkg '*/*' 

# Clone the cmaketools repo

git clone https://github.com/gartung/cmaketools.git

# Make a build directory and run CMake with the defines needed to find the header files used in dictionary generation

cd ..
mkdir build
cd build
cmake ../src  \
-DBoost_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/boost/1.72.0-gchjei/include \
-DROOT_DIR=/build/cmssw/cc8_amd64_gcc8/lcg/root/6.20.06-ghbfee5/cmake \
-DCMakeTools_DIR=../src/cmaketools \
-DROOT_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/lcg/root/6.20.06-ghbfee5/include \
-DMD5_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/md5/1.0.0-bcolbf/include \
-DTBB_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/tbb/2020_U2-ghbfee/include  \
-DTINYXML2_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/tinyxml2/6.2.0-ghbfee/include \
-DSIGCPP_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/sigcpp/2.6.2-bcolbf2/include/sigc++-2.0 \
-DHEPMC_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/hepmc/2.06.07-bcolbf2/include  \
-DXERCESC_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/xerces-c/3.1.3-bcolbf/include \
-DFMT_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/fmt/7.0.1/include \
-DCUDA_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/cuda/11.0.3/include \
-DEIGEN_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/eigen/d812f411c3f9-ghbfee/include \
-DFASTJET_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/fastjet/3.3.4/include \
-DCLASSLIB_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/classlib/3.1.3-ghbfee/include  \
-DORACLE_INCLUDE_DIR=/build/cmssw/cc8_amd64_gcc8/external/oracle/12.1.0.2.0-bcolbf/include
make VERBOSE=1 -j8

# Assuming the configuration and build complete you can now make the dictionaries available by setting LD_LIBRARY_PATH

LD_LIBRARY_PATH=$PWD/lib
