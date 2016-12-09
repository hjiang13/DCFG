The repository contains source code for a tool to create dynamic control- and 
data-flow graph with memory trace and NUMA/cache access behavior of a sequetial
and parallel program. The tool is developed on top of pintool for binary 
instrumentatio (http://pintool.org) and dyninst for binary analysis (http://www.dyninst.org/). 
You need to install the latest pintool and dyninst to make the program functional. 

### For installation on Linux

1. Download the latest pintool from http://www.pintool.org (currenly using rev 76991, version 3.0). 
The website also provide tutorial and guide for using pin.

1. Unzip the pintool and navigate to the source/tools folder of pinplay. Under the tool folder, 
clone this rep (https://github.com/passlab/DCFG). The DCFG compilation leverages pintool building framework.
So this is the easiest approach to have it running.

1. "make" command will create the pin tool binaries in the folder, including edgecount, calltrace and 
pinatrace (memory trace). You can execute the pintool with those examples to generate edgcount, calltrace and 
memory trace files for a sample program (hello, which is generated by "gcc hello.c -o hello"). The three tracing files are 
text files (calltrace.out  edgcnt.out  pinatrace.out) that can be viewed using a text viewer (notepad, vi, cat, less, etc). 

        ../../../pin -t obj-intel64/edgcnt.so -- ./hello
        ../../../pin -t obj-intel64/pinatrace.so -- ./hello
        ../../../pin -t obj-intel64/calltrace.so -- ./hello

    Those examples are modified from examples of pin distributions. You can find other examples in the source/tools folder
    Check the [pintool guide](https://software.intel.com/sites/landingpage/pintool/docs/76991/Pin/html/) for more information. 
    For example, The [pinatrace memory trace example](https://software.intel.com/sites/landingpage/pintool/docs/76991/Pin/html/index.html#MAddressTrace).

1. There are two python scripts (callgraph.py and flowgraph.py) for generating the callgraph and control-flow 
graph using the tracing data and objdump and sym info of the hello binary. Run the script to see the required input of 
the python scripts. The objdump and sym file of the hello program can be generated using objdump command and readelf command. 
Please check objdump-routine.csh script for using objdump to generate the dump needed. The repo already included the pre-generated
tracing files, objdump (hello.s) and sym files (hello.sym and hello.main.sym). Currently the callgraphy.py generates the 
control flow in graphml and callgraph.py generating vcg which has not yet been well tested. 


### For generating static control flow graph using dyninst
The dyninst_CFG folder contains sources for generating dot-based CFG using dyninst and you need to follow
dyninst installation guild to make it work. Check the README.md file in the dyninst_CFG folder.
