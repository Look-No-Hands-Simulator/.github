## Hello there! :)
## This is the Look No Hands Formula Student Driverless Simulator, it was developed with support from Oxford Brookes University as a dissertation project and for Oxford Brookes Racing: Autonomous, the university's FSAI (FSD) team. But is open source for all teams, all over the world, and you can use it if you are not on a team too or whoever you are (as long as you don't use it for profit maybe)?
## Please feel free to fork and add things to it or change it once it is submitted!!! 
## I believe in the progress of improving safety in vehicles to prevent crashes and electrification of cars to reduce pollution. I hope these things can motivate you if you work in this area!

## Aimed System Requirements (may work on other systems)
Ubuntu 20.04. 
ROS2 Foxy.
Unity ver 2022.3.11.+.
Rviz2.

- Install Ubuntu 20.04 by having an empty USB stick, downloading Ubuntu onto it using a software that can flash Operating System images onto SD cards and USB devices such as [Rufus](https://rufus.ie/en/) or [Balena Etcher](https://etcher.balena.io/), plug it into a computer and boot into the USB drive, now create a dual boot by splitting the memory (Be careful! If you do this wrong by selecting a drive or memory location which is already in use and overwrite over it then you can overwrite and delete files on your computer so make sure if you have important things on there then maybe back them up), or alternatively download it onto an external SSD drive.
- Install ROS2 Foxy here https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html

## How to use
- If you are using this project in any way please fork one of the repositories for reference that you are using it. I think unityros-ws or unity-assets may be good repositories to fork. Given there are many repositories you may want to commence with cloning thereafter to use the yaml file with vcstool to pull the rest of the repositories into your workspace (keep reading). Please don't use this project in your dissertation if you are writing one or any public projects until after 2024 September 30th (graduation date) whence you are free to use it with credits (a link to the repository or see near bottom of the page for additional names).   
- Navigate to [unityros-ws](https://github.com/Look-No-Hands-Simulator/unityros-ws) on Github and clone this repository into a folder with `git clone https://github.com/Look-No-Hands-Simulator/unityros-ws` in your terminal in the chosen directory.
- Then follow the instructions inside its README.md on your Ubuntu computer and it will create a ROS2 workspace and pull the rest of the repositories. source ROS2 with `source opt/ros/foxy/setup.bash`. Or replace foxy with your distro.
- Please then build the workspace with `colcon build --symlink-install` in the terminal at the root of 'unityros-ws' folder.
- and now you should be able to use the simulator's ROS2 nodes by sourcing the setup.bash file with `source ./install/setup.bash` (make sure you are in the directory above the install folder that was built, therefore probably in rosunity-ws root).
- and then use `ros2 run ros_tcp_endpoint default_server_endpoint` to run the ROS-TCP-Connector endpoint node and start the server in a new terminal.
- then you can open unity-assets (the Unity project folder) in Unity.
- Now you must create your own launch file if you want to use your pipeline with it to include your nodes.
- If you are having trouble please make sure you remembered to source ROS2 with `source opt/ros/foxy/setup.bash`.
- It's probably best to keep your software pipeline ROS2 code in a seperate workspace folder therefore you can `source ./install/setup.bash` source it whilst also sourcing the unityros-ws and then use both at the same time, remember you'll need to source them in every new terminal you open.

## Recommendations for running a system with the right requirements
I recommend you to use an external SSD with a SATA to USB-C cable (USB-C will transfer data faster than USB-A), on this SSD install Ubuntu and thus you can boot it from plugging it into your personal computer and starting it up, then entering into SSD from the boot menu. This requires you to enter the boot menu of your personal computer by pressing a button such as F11 repeatedly on startup then disabling secure boot from the menu options and adding the SSD as a bootable drive option, saving, and restarting the PC. Alternatively you may wish to dual boot, which means you can use two operating systems on your computer but you choose which one to use when booting up each time.

## Packages to install
Make sure you have https://github.com/Unity-Technologies/ROS-TCP-Connector by following the graphical instructions to add this package inside Unity.
//Add shell files//
//Add Disc image file//

## What the simulator includes
- Simulated sensors that publish to topics including: LiDAR, IMU, GPS, Wheelspeeds, Stereo camera, Depth maps, Ground truth position. With gaussian noise and covariance options.
- RVIZ2 visualization of sensor data.
- A physics vehicle model of the ADS-DV with 4 wheel power and ackermann steering.
- Vehicle model keyboard control for braking, steer, acceleration (space = brake, w = acceleration, s = reverse if enabled) with published control values on ROS2 topics.
- Vehicle model control through ROS2 subscription to topics reading ADS_DV_Msgs type commands (ADS_DV_DriveF, ADS_DV_Steer, ADS_DV_Brake) to move the vehicle. The ADS-DV simulated subscribes to `/AI2VCUSteer` , `/AI2VCUDriveF` , `/AI2VCUDriveReverse` (if reverse included) , `/AI2VCUBrake` , The names of each of these can be changed within Unity by selecting CAR-ROOT object and changing the values within the Car Control script inside the Inspector.
- Generation of cone track maps with a selection menu.
- Day and night cycle.
- Speedometer.

## What is formula Student Driverless?
It's a student competition for creating autonomous racing cars in university teams created by IMechE. 
https://www.imeche.org/events/formula-student/team-information/fs-ai

## What's the purpose of this simulator?
It is to help teams to test their ROS2 based algorithms by creating simulated sensor data that can publish onto topics that can then be used by algorithms to send back control commands by publishing ADS_DV_Msgs topics which the simulator will subscribe to and actuate the car in Unity to accelerate, brake. The simulator aims to have different environments and interface with missions. 

## What does a general software pipeline I can plug into this look like?
You would generally either take a complete machine learning approach or standard classical pipeline with different algorithms, although generally any algorithm stack will always follow a 'sense, plan, act' methodology. But if you follow Formula Student Driverless Germany there are many great presentations and documents on creating a pipeline.

Which looks like this -> 
- **Mission and state control**: You would probably make a ROS2 launch file to launch the appropriate software nodes you need for the particular mission you choose to execute for this launch file (skidpad or acceleration etc.). In there you would also need to make sure to run the node ROS-TCP-Endpoint from this simulator if you wanted to use it whence you can then run the unity-assets project to start the simulator. You may also need a state machine to check what state your system is in and what it should be doing, also for safety if the emergency brake is pressed then the system should go into shutdown.
- **Perception**: Read data from your sensors that percieve the world, either the stereo camera, LiDAR, (or more uncommonly RADAR, Infrared), a combination is the best approach, and then you would identify the landmarks in the world using computer vision algorithm such as YOLO, create bounding boxes to identify cone colours (classifying objects) and position relative to camera, you might also use a depth map to estimate the depth/distance to the cones, from all of this your algorithm/s should return (x,y,colour) of the cones. A stereo camera can use triangulation to estimate distance. You might also use the LiDAR which produces pointclouds here which you could identify cones and their depth/distance from the density of points and shape using a point based neural network. You may need to calibrate your sensors, correct errors, perhaps fuse data of different sensors with sensor fusion as they return different formats of data at different times, a kalman filter is good for this and for fixing the error caused by the inherent noise from sensors. You might also cluster data to ensure accuracy of cone detection using some clustering algorithm.
- **Localization and mapping**: given the local 'can see right in front of the car' data from the vision sensors you can now combine this with odometry sensors such as the IMU, Wheelspeeds, GPS -> which are providing motion data. You will want to know where the car is in the world/map (localization) whilst creating a map of the world. You might use a SLAM algorithm to do this and combine the odometry data with the observations (vision data). A kalman filter/sensor fusion technique (often inside the SLAM) is often used here if it was not used earlier because the odometry sensors have a lot of noise and cumulative errors that are better when fixed.
- **Path planning**: Given you know the location of cones and the car or perhaps a local or global map you will now want to plan a path for the car through this world. You may go through the center or you may create a racing line. If you were to imagine the map in a 2D way you could use delaunay triangulation on the cones to create an understanding of the driveable path. You could also use any search algorithm such as A*.
- **Control**: Now that you have created a path of perhaps waypoints or splines you want to control the vehicle to move to these waypoints etc. and thus you might use either a PID or MPC controller which are controllers that will be fed back the errors in the way the car responds through braking, throttle, steering, (given the dynamics will mean the movements are not perfect as you command) to keep following a look-ahead point and reach the goals. You will also need to probably communicate to the car from the PC through a CAN BUS network and therefore the signals will have to be converted to ones the hardware controllers can understand but the ADS-DV will do this for you so unless you are making your own driverless vehicle this part you can use the ADS-DV interface, this simulator also does abstract the detail of the hardware controllers which would exist in the real world. 

## Credits
Various open source tools have been used in this project or items created by others with permission, they include:
- Unity Game Engine: https://unity.com/
- Unity ROS-TCP-Connector: https://github.com/Unity-Technologies/ROS-TCP-Connector
- Lidar: https://github.com/sudhirpratapyadav/unity_ros_lidar_3d
- FSAI API: https://github.com/FS-AI/FS-AI_API
- ADS-DV CAD model: https://github.com/FS-AI/FS-AI_ADS-DV_CAD
- Depth camera: Unity's ImageSynthesis package
- The JSON files of cone tracks were made by an alumni of OBRA: [Belle Garlick](https://github.com/BelleGarlick) who is also working on a great project you should check out!
- The cone 3D models and blue/red ADS-DV texture were made by an alumni of OBRA: [Jordan Trainor](https://www.linkedin.com/in/jordantrainor/)
- ADS_DV_msgs.msg XML were first generated by an alumni of OBRA: [Jacob Culley](https://github.com/jacobculley)
- These two developers added code in the early stages as a spinning selection menu and asphalt ground and a connector to Gazebo and fixes, some of this code may be available or unavailable but they were a part of this project while at OBRA: [Tony South](https://github.com/t-south) (who is also working on a project you should check out too!) and [Elias Fandi](https://github.com/eliasfandi)
- The simulator was inspired by the Gazebo simulator made by older OBRA alumni, the way this simulator connects with ROS2 was heavily inspired by it, accredited to [Jacob Culley](https://github.com/jacobculley),[Elias Fandi](https://github.com/eliasfandi),[Jordan Trainor](https://www.linkedin.com/in/jordantrainor/),[Enric Gil](https://www.linkedin.com/in/enric-ge/)

- With big thanks to all support and support over the years at university. Including all OBRA friends, family, friends, supervisor, and teachers. :)  

Resources and tutorials that were a great help:
- Unity wheel colliders model: https://www.homeandlearn.co.uk/games-programming/unity-wheel-colliders.html

**I think Unreal engine would have been better suited for this project therefore if you are thinking of doing a similar project I recommend you to use Unreal engine for its superior performance (C++), automotive support, and better lighting and destruction system. A simulator like this has already been created here https://fs-driverless.github.io/Formula-Student-Driverless-Simulator/v2.2.0/software-install-instructions/ and Formula Student Driverless Simulator is very well documented and based on AirSim by Microsoft https://github.com/microsoft/AirSim/tree/main!**

## Where did the funny name come from?
At my time at Oxford Brookes Racing: Autonomous this joke was made because the cars are autonomously driven. 

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
