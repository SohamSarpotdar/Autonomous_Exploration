



# Autonomous Exploration using Turtlebot <img src="https://user-images.githubusercontent.com/92629417/197411798-d35da8fb-9153-4104-9faa-556a2e9cdeab.gif" width="35" height="32" />  <img src="https://user-images.githubusercontent.com/92629417/197412192-87d76ad9-b654-4701-9e0f-12b7c35552b6.gif" width="35" height="32" /> 

## Table of Contents 
- [Description](https://github.com/SohamSarpotdar/Autonomous_Exploration#description-robot)
- [Turtlesim](https://github.com/SohamSarpotdar/Autonomous_Exploration#turtlesim-turtle)
- [Turtlebot3 Simulations and Mapping](https://github.com/SohamSarpotdar/Autonomous_Exploration#turtlebot3-simulation-and-mapping)
- [Docker](https://github.com/SohamSarpotdar/Autonomous_Exploration#docker-)
- [Results](https://github.com/SohamSarpotdar/Autonomous_Exploration#results)
  - [Avoiding Obstacles](https://github.com/SohamSarpotdar/Autonomous_Exploration#avoiding-obstacles--)
  - [Maps](https://github.com/SohamSarpotdar/Autonomous_Exploration#maps-of-a-corner-of-lab--)
- [Looking Forward to](https://github.com/SohamSarpotdar/Autonomous_Exploration#looking-forward-to--)

## Description :robot:

<img src="https://user-images.githubusercontent.com/92629417/197410812-79a8e4d7-0d01-465a-ab1f-d3432ba14ab7.gif" width="795" height="400" />

This project uses Robot Operating System(ROS) to move Turtlebot autonomously in an unexplored area with the help of [LiDAR](https://www.ydlidar.com/products/view/5.html) and at the same time create a map of the area. 

## Turtlesim :turtle:

To understand some basic functionalities of [rospy](http://wiki.ros.org/rospy) library which is used throughout this project and velocity control of a robot, Turtlesim node is used.

Tracing some common shapes - 

<img src="https://user-images.githubusercontent.com/92629417/197455894-23a603e1-9239-4745-900d-45690bd41a75.gif" width="260" height="260" /> <img src="https://user-images.githubusercontent.com/92629417/197455897-aa6f057d-232e-444d-80ae-d93939ea146e.gif" width="260" height="260" /> <img src="https://user-images.githubusercontent.com/92629417/197455902-295241d9-73ad-4eab-867c-f90efeb2f81a.gif" width="260" height="260" />

Applying P controller to control the turtles - 

<img src="https://user-images.githubusercontent.com/92629417/197455887-3a734f2d-c62f-4995-972f-692ed789c3e1.gif" width="260" height="260" /> <img src="https://user-images.githubusercontent.com/92629417/197455890-ee2e2415-a235-4bce-951c-9727fa2afd20.gif" width="260" height="260" /> <img src="https://user-images.githubusercontent.com/92629417/197455895-86bd9a2a-42df-4db1-8d2a-657670bb71f1.gif" width="260" height="260" />

## Turtlebot3 Simulation and Mapping
We first performed teleoperation(operating manually through keyboard) and both mapping techniques in simulation and then we implemented the same on hardware.  

### Teleoperation - 

<img src="https://user-images.githubusercontent.com/92629417/197505977-3fdeaa08-2800-4817-8a8e-3d43cf1e60b4.gif" width="775" height="450" />

### Hector mapping - 

<img src="https://user-images.githubusercontent.com/92629417/197514237-3412ad9a-a43d-4632-84fe-2f55bfd28662.gif" width="775" height="450" />

In hector-slam, it uses previous scan results to estimate the current state of the system. So a drift from the beginning will be recorded and results in a random rotation and translation of the map frame against other ground truth frames

### Gmapping -

<img src="https://user-images.githubusercontent.com/92629417/197510766-f0a685ce-dfee-46c4-8dbf-706d42d9e39b.gif" width="775" height="450" />

## Docker <img src="https://user-images.githubusercontent.com/92629417/197572181-a6bd28c5-6a82-4978-990f-806e2162290a.png" width="33" height="23" />

To run the code on Turtlebot2, we used ROS melodic installed in a Docker container.

To setup the Docker Container and connect to Turtlebot2  
- Install [Docker](https://docs.docker.com/engine/install/) on your device
- Open the Turtlebot2.zip folder, provided in this repository, in VsCode
- Build the container and try resolving the errors, if any 
- In new Terminal, Run the command ``` bash .devcontainer/post_create_commands.sh``` 
- Connect the Kobuki cable to your pc and in new terminal run ``` roslaunch turtlebot_bringup minimal.launch```

## Results
We finally deployed our code on Turtlebot2 and, after facing some issues and refactoring the code, we got the following results - 

### Avoiding Obstacles - 

<img src="https://user-images.githubusercontent.com/92629417/197415431-5d706210-aaee-475d-a602-25d47e0e69dd.gif" width="380" height="420" /> <img src="https://user-images.githubusercontent.com/92629417/197417790-4b180820-5ce3-470d-84f3-7ccb0ca5a69d.gif" width="390" height="420" /> 

The ranges' list in LiDAR [data](http://docs.ros.org/en/melodic/api/sensor_msgs/html/msg/LaserScan.html) has a length of 720. Central region is defined in first 40 values and last 40 values which would correspond to 20 degrees left and right of the normal line to the robot. Left and Right regions are defined by next 140 values from beginning and end of the list respectively. Average value of range is found in each of these regions and if found less than the safe distance of robot from an obstacle, in any region then move in turn or move in some other direction.

As we used only one sensor in this project, which is LiDAR, only hector mapping was possible.

### Maps of a Corner of Lab - 
<img src="https://user-images.githubusercontent.com/92629417/197415492-eb471516-4029-4210-a3a0-73b90232bbb4.PNG" width="380" height="350" /> <img src="https://user-images.githubusercontent.com/92629417/197415484-4bcf2629-d223-4d5b-bb7f-dd3a98e8d82f.PNG" width="380" height="350" />

### Maps of other parts - 
<img src="https://user-images.githubusercontent.com/92629417/197415489-86161f30-7bc2-4045-9f5c-5765d663839a.PNG" width="380" height="350" /> <img src="https://user-images.githubusercontent.com/92629417/197415490-6814b7ba-1bd9-4cf7-899a-8e849c4d1e0d.PNG" width="380" height="350" />

## Looking Forward to -
- Removing Distortions in the maps
- Applying Path Planning [Algorithms](https://en.wikipedia.org/wiki/Motion_planning#Algorithms)
