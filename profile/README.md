## Hello there! :) 
## This is the Look No Hands Formula Student Driverless Simulator, it was developed with support from Oxford Brookes University as a dissertation project and for Oxford Brookes Racing: Autonomous, the university's FSAI team. But is open source for all teams, all over the world, and you can use it if you are not on a team too or whoever you are as long as you don't use it for profit.
## Please feel free to fork and add things to it or change it once it is submitted!!!

## Aimed System Requirements (may work on other systems)
Ubuntu 20.04. 
ROS2 Foxy.
Unity ver 2022.3.11.
Rviz2.

## Recommendations for running a system with the right requirements
I recommend you to use an external SSD with a SATA to USB-C cable (USB-C will transfer data faster than USB-A), on this SSD install Ubuntu and thus you can boot it from plugging it into your personal computer and starting it up, then entering into SSD from the boot menu. This requires you to enter the boot menu of your personal computer by pressing a button such as F11 repeatedly on startup then disabling secure boot from the menu options and adding the SSD as a bootable drive option. Alternatively you may wish to dual boot.

## What is formula Student Driverless?
It's a student competition for creating autonomous racing cars in university teams created by IMechE. 
https://www.imeche.org/events/formula-student/team-information/fs-ai

## What's the purpose of this simulator?
It is to help teams to test their ROS2 based algorithms by creating simulated sensor data that can publish onto topics that can then be used by algorithms to send back control commands by publishing ADS_DV_Msgs topics which the simulator will subscribe to and actuate the car in Unity to accelerate, brake. The simulator aims to have different environments and interface with missions. 

## How to use

## Credits
Various open source tools have been used in this project or items created by others with permission, they include:
- Unity Game Engine: https://unity.com/
- Lidar: https://github.com/sudhirpratapyadav/unity_ros_lidar_3d
- FSAI API: https://github.com/FS-AI/FS-AI_API
- ADS-DV CAD model: https://github.com/FS-AI/FS-AI_ADS-DV_CAD
- Depth camera: Unity's ImageSynthesis package
- The JSON files of cone tracks were made by an alumni of OBRA: [Belle Garlick](https://github.com/BelleGarlick)
- The cone 3D models and blue/red ADS-DV texture were made by an alumni of OBRA: [Jordan Trainor](https://www.linkedin.com/in/jordantrainor/)
- These two developers added code in the early stages as a spinning selection menu and asphalt ground and a connector to Gazebo and fixes, some of this code may be available or unavailable but they were a part of this project while at OBRA: [Tony South](https://github.com/t-south) and [Elias Fandi](https://github.com/eliasfandi)
- The simulator was inspired by the Gazebo simulator made by older OBRA alumni, the way this simulator connects with ROS2 was heavily inspired by it, accredited to [Jacob Culley](https://github.com/jacobculley),[Elias Fandi](https://github.com/eliasfandi),[Jordan Trainor](https://www.linkedin.com/in/jordantrainor/),[Enric Gil](https://www.linkedin.com/in/enric-ge/)

- With big thanks to all support.

Resources and tutorials that were a great help:
- Unity wheel colliders model: https://www.homeandlearn.co.uk/games-programming/unity-wheel-colliders.html

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
