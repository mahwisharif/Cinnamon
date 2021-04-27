This directory contains the code for Cinnamon language compiler

## Section 1: Cinnamon Build Instructions: 

Cinnamon can currently target three different binary frameworks; ``Janus``, ``Intel Pin`` and ``DynInst``. In order to build compiler 

`$ export CINNAMON_ROOT = /path/to/cinnamon-source`

`$ cd $(CINNAMON_ROOT)`

To build cinnamon backend for Janus

``$ make TARGET=janus``

To build cinnamon backend for Pin

``$ make TARGET=pin``

To build cinnamon backend for DynInst

``$ make TARGET=dyninst``

## Section 2: Compile Sample Program using Cinnamon:

Cinnamon sample programs are available under tests/ directory.
The following commands will compile cinnamon program `ins.dsl` and integrate the resulting code into respective frameworks. You will need to set the path to your target framework installation in the respective scripts.

``$ $(CINNAMON_ROOT)/Scripts/compileToJanus.py $CINNAMON_ROOT/tests/ins.dsl``

``$ $(CINNAMON_ROOT)/Scripts/compileToPin.py $CINNAMON_ROOT/tests/ins.dsl``

``$ $(CINNAMON_ROOT)/Scripts/compileToDyninst.py $CINNAMON_ROOT/tests/ins.dsl``


After this, the final tool can be built and run using the target framework's build instructions.


if you just want to compile the `cinnamon` code and not yet intergate in target framework, run the following command. this will generate a number of different files containing relevant code for the cinnamon program  

``$ cd $CINNAMON_ROOT``

``$ ./bdc $CINNAMON_ROOT/tests/ins.dsl``


## Section 3: Cinnamon Janus Implementation: 

You can get the `Janus` implementation with placeholders, templates and utility libraries for `Cinnamon` from https://github.com/mahwisharif/Janus.git and switching to 'cinnamon' branch. 

``$git clone https://github.com/mahwisharif/Janus.git``

``$cd Janus``

``$git checkout -b cinnamon origin/cinnamon``

Once the code for janus has been generated and integrated by running `compileToJanus.py` script in Section 2, you can build the final tool using the following commands: 
``$ (cd build; cmake ..; make -j8)``

**NB**: you will need to set the `JanusPath` in `compileToJanus.py` to where you cloned the `Janus` code.


run the final tool on target binary 

``$ ./janus/jdsl_run <target_binary>``

## Section 4: Cinnamon Pin Implementation: 

You can get the relevant files for `Pin`  with placeholders, templates and utility libraries for `Cinnamon` from https://github.com/mahwisharif/pin-cinnamon

Copy ``MyDSLTool`` folder from ``pin-cinnamon`` under ``path-to-your-pin-root-dir/source/tools``

in ``compileToPin.py``, set ``PinPATH=your-pin-root-dir/source/tools/MyDSLTool``

Once the code for `Pin` has been generated and integrated by running `compileToPin.py` script in Section 2, you can build the final tool using the following commands:

``$ cd your-pin-root-dir/source/tools/MyDSLTool``

``$ make obj-intel64/MyDSLTool.so``

run the tool using the following command 

``$ your-pin-root-dir/pin -t obj-intel64/MyDSLTool.so -- <target_binary>``

