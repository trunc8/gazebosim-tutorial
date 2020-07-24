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
    - Start Gazebo paused:
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
    - Downloaded .STEP file from [Velodyne website](https://velodynelidar.com/wp-content/uploads/2019/09/HDL32E_Outline_Model.step) -> Freecad(to export in Collada(.dae) format) -> Blender(to scale and rotate) 
    - Vertical offset: Mesh's coordinate frame does not exactly match up with the coordinate frame of the SDF link
3. Control Plugin
    - Aim: Use a simple PID controller to control the joint's velocity via Model Plugin
    - Three ways of specifying velocity:
        1. Hardcode velocity in .cc file
        2. Pass velocity as parameter in sdf file
        3. Pass velocity dynamically as some API request
    - For the first way, just minor modifications in velodyne\_plugin.cc needed
    - For the second way, small changes in velodyne.world and velodyne\_plugin.cc needed
    - For the third way, made a new file vel.cc (acts as a publisher), edited velodyne\_plugin.cc (acts as a subscriber) and added a line in CMakeLists.txt
    - Dynamic adjustments require the addition of an API. These are of two types:
        1. Message passing [Gazebo's transport mechanism]
        2. Functions [most often used when interfacing Gazebo to ROS]
4. Connect to ROS
    - We placed hooks to a robot middleware, i.e. ROS

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
4. Hello\_World Plugin
    - hello\_world.cc
        - namespace gazebo
        - Inherit WorldPlugin
        - void Load(physics::WorldPtr _world, sdf::ElementPtr _sdf)
        - GZ_REGISTER_WORLD_PLUGIN({Plugin\_Class\_Name})
    - CMakeLists.txt
    - hello.world
    - Creating and cd'ing into build directory:
    > $ cmake ../<br/>
    > $ make
    - gzserver
5. Model\_Push Plugin (Model Plugin)
    - model\_push.cc
        - ModelPtr
        - ConnectionPtr
    - mode\_push.world
6. Programmatic World Control (World Plugin)
    - world\_edit.cc (this example programmatically modifies gravity)
7. Sytem\_GUI Plugin (System Plugin)
    - system\_gui.cc (this example is plugin for gzclient that saves images into a specific directory)
    - Not working as expected; Keeps crashing
