# Gazebosim_Tutorial
Notes and files written by me while completing [tutorials](http://gazebosim.org/tutorials) on [Gazebosim](http://gazebosim.org/)

### Beginner Level
1. Blob-following robot
	- Built in Model Editor (Ctrl+M)
	- Used pre-defined plugin libFollowerPlugin.so (so=shared object)
	- Left "Innerxml" field blank
2. Hollow wheel
	- First built svg file using Inkscape SVG Editor
	- Extruded svg file inside Gazebo's Model Editor
3. Robot House
	- 2-storeyed house using downloaded floorplan
	- Used Building Editor (Ctrl+B)

### Intermediate Level
1. Constructing Velodyne LiDAR
	- Start Gazebo paused
	> $ gazebo velodyne.world -u
	- .world file relevant tags:
		1. collision
		2. visual
		3. inertial
		4. joint
		5. sensor
		6. noise
2. Model Appearance
	- Gazebo can only use STL, OBJ or Collada files for meshes
	- Used downloaded .STEP file -> Freecad(export in Collada(.dae) format) -> Blender(scale and rotate) 
	- Vertical offset: Mesh's coordinate frame does not exactly match up with the coordinate frame of the SDF link

### Write A Plugin: Tutorial
1. A plugin is a C++ library that is loaded by Gazebo at runtime
2. Previous versions of Gazebo utilized controllers (these were statically compiled into Gazebo). In comparison, plugins are more flexible
3. 6 types:
	1. World: control world properties (such as physics enginer, ambient lighting, etc.)
	2. Model: control joints, and state of model
	3. Sensor: acquire sensor information and control sensor properties
	4. System
	5. Visual
	6. GUI
4. HelloWorld Plugin
	- hello_world.cc
	- CMakeLists.txt
	- Creating and cd'ing into build directory
	> $ cmake ../<br/>
	> $ make
	- gzserver

	

