RMASBench: Multi-Agent Coordination Benchmark
=============================================

This is the main repository of the RMASBench benchmarking tool. There's actually no code in this repository, but it contains git submodules of all necessary software to run the platform and all available algorithms.

Installation
------------

Check out this repository and all its submodules to your computer::

	git clone --recursive https://github.com/RMASBench/RMASBench.git

You will get an RMASBench folder containing 4 sub-folders (projects):

- **BinaryMaxSum.** 
	Library that implements a binary version of MaxSum, including special factors whose messages can be computed more efficiently.

- **RSLB2.**
	Main tool of the RMASBench platform. This is where most of your work and test will take place, as it allows for an easy interfacing with the robocup rescue simulation platform.

- **jmaxsum.**
	Library that implements the standard MaxSum version. It includes a (D)COP solver and the bounded MaxSum algorithm as well.

- **roborescue**
	Robocup Rescue agent simulation platform.

All this software must be compiled being able to run the *RSLB2* tool. This can be easily achieved by using ant with the proper target for each subfolder::

	cd BinaryMaxSum; ant jar; cd ..
	cd jmaxsum; ant jar; cd ..
	cd roborescue; ant oldsims jar; cd ..
	cd RSLB2; ant jar; cd ..

If everything compiles well (you can ignore warnings), you are now ready to start testing. 


Usage
-----

Normally, you will run experiments from within the *RSLB2/boot* folder. Get into that folder and check out the launcher's options::

	cd RSLB2/boot
	./start.sh -h

You can now launch an example scenario using any of the included algorithms. When testing, include the "*-v*" flag to enable the simulation viewer. For example, you can run the example scenario with agents coordinated by the MaxSum algorithm::

	./start.sh -v -a MaxSum

**Warning:** The first time you run a scenario of a map (default is "paris"), the simulator will pre-compute a number of things about the map. This process takes around 5 minutes, during which the program will seem to freeze. If you want to see the process, open a new terminal, move to the *boot* folder and execute::

	tail -f logs/*/fire-out.log