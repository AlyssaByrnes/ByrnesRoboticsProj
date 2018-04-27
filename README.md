# ByrnesRoboticsProj

A lot of this work and README was taken and modified from [Apex](https://github.com/mlab-upenn/arch-apex).

# Installation

## Dependencies - SWIG and Armadillo

`brew install swig` 

`brew install armadillo`

## Build Trajectory Generator Library and Wrap in Python

### Create interface:
`swig -c++ -python trajectorygenerator.i`

### Build library and link armadillo:
`g++ -fPIC -c trajectorygenerator.cpp -O2 -larmadillo`

### Build wrapper:
`g++ -fPIC -c trajectorygenerator_wrap.cxx -I/usr/lib/python2.7 -O2 -larmadillo`

Note: make sure that the Python.h file path is right. usually in most systems you will have to change to pythonX.X/Python.h

### Build file containing specific function which we will expose to APEX tool:
`g++ -fPIC -c libtraj_gen_v2.cpp -O2 -larmadillo`

### Link:
`g++ -shared trajectorygenerator.o libtraj_gen_v2.o trajectorygenerator_wrap.o -L/usr/lib/python2.7 -lpython2.7 -o _trajectorygenerator.so -O2 -larmadillo`
 
### Make APEX.py executable:
`chmod +x APEX.py`

### Run APEX:
`./APEX.py`
