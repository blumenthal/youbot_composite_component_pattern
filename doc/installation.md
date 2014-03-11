Installation guide
------------------

 * Dependencies
  * [Clang](#clang) 
  * [Luajit](#luajit)
  * [Soem](#soem)
  * [KDL](#KDL)
 * youBot demo
  * [Microblx](#microblx) 
 * [Example usage](#example-usage)
 
Here is a summuary on how to install the youbot example  on Ubuntu (12.04)

Dependencies:

## Clang 

```
	sudo apt-get install clang
```

## Luajit
 
```
	wget luajit.org/download/LuaJIT-2.0.2.tar.gz
	tar -xvf LuaJIT-2.0.2.tar.gz 
	cd LuaJIT-2.0.2
	make
	sudo make install
	sudo ln -s /usr/local/bin/luajit /usr/local/bin/lua
	sudo ldconfig
```

## Soem
 
```
	git clone https://github.com/kmarkus/soem1.2.5.git
	cd soem1.2.5/src
	make
```	
 
## KDL
 
 ```
 	git clone http://git.mech.kuleuven.be/robotics/orocos_kinematics_dynamics.git
 	cd mkdir build
 	orocos_kdl
 	cd build
 	cmake ..
 	make
 	sudo make install
 ```

## Microblx
Installation of the actual microblx library with enabled youbot driver ans kindyn package:
```
	git clone https://github.com/kmarkus/microblx.git
	git checkout dev # you might want to skip this step
```

Then go to the youbot_driver folder:

```
	cd <microblx_path>
	cd std_blocks/youbot_driver

```

Here you have to create a symbolic link to the folder of the soem library:

```
	ln -s <path_to_soem>/soem1.2.5 soem
```

Compile the microblx software: 

```
	cd <microblx_path>
	source env.sh 
	make HAVE_KDL=1
	echo "export MICROBLX_DIR=$PWD" >> ~/.bashrc
```

Then grant correct permissions to the luajit binary:

```
	sudo setcap cap_sys_nice,cap_net_raw+ep /usr/local/bin/luajit-2.0.2 
```

## Example usage

Start the test with (the -i parameter brings in the interactive console to provide further commands.)
```
	luajit -i examples/youbot_test.lua
```

Then type the command for calibating the are. 
This __HAS DO BE DONE__ after each power-down and __BEFORE__ using any other arm functions
```
	arm_calibrate()
```

Some function e.g. to move the arm are;

```
	arm_home()
	arm_tuck()
```

