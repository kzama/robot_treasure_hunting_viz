# robot_treasure_hunting_viz

This is a treasure hunting game visualization, aided by a robot. 
We assume 4 objects, easily being lost in a house environment and we display them in a gui. 
The user can choose an object which represents the "hidden treasure".
The users can navigate the robot in a place, where the map is provided.
The robot marks the range, indicating the area where the treasure can be located. 
The closer the robot reaches the treasure, the minimum the range becomes.
The marking colors in the range denote the "hot" and the "cold" area, depending on the distance between the robot and the treasure.

Tested on:
* Ubuntu 16.04
* ROS Kinetic
* Turtlebot

## Requirements
* Python (>= 2.7)
* full package of ros (gazebo, rospy, catkin workspace been set)
* rviz
* ros-turtlebot . E.g: 
    ```
    sudo apt-get install ros-kinetic-turtlebot-*
    ```

    
## Installation

* Clone the current repository to your catkin workspace. 
* Then build your catkin workspace:
    ```
    cd ~/catkin_ws/
    catkin_make
    ```

## Useful Parameters

You can modify some parameters of the game if you wish.

1. Change treasure position.
If you want to "hide" some treasures on your map, set a point at the *robot_treasure_area/config/parameters.yaml* file like the example below:
  * treasure_locationN_x: -1.38479661894
  * treasure_locationN_y: 2.86624727474

  , where x, y are the x-,y- coordinates respectively and ***N*** is the increment identification number of the treasure (N >=1 and N<=4). 

2. Synchronize with the frame id of rviz. At the ***frame_id*** parameter of the the *robot_treasure_viz/config/parameters.yaml* file, set the same id as it is defined  in the *Global Option > Fixed Frame* of rviz

3. Specify the boundary of "hot" and "cold" area, depending on your world. Go to *robot_treasure_viz/config/parameters.yaml*  file and change the parameter ***state_limit*** (in meters).

4. Specify a "comfort zone" to create a bigger coverage range, thus the treasure is surely into the visualized area. Go to *robot_treasure_viz/config/parameters.yaml*  file and change the parameter ***extra_range*** (in meters).

5. Specify a maximum distance of the coverage range, depending on your world. Go to *robot_treasure_viz/config/parameters.yaml*  file and change the parameter ***max_radius*** (in meters).

## Execute the application on a gazebo environment:

Firstly you should define your world through gazebo and create a map for it. For more information about it, please refer to [ROS Wiki](http://wiki.ros.org/turtlebot_gazebo/Tutorials/indigo/Explore%20the%20Gazebo%20world).

Then execute the following:

1. On a terminal, run your world in gazebo for the turtlebot:
    ```
    roslaunch turtlebot_gazebo turtlebot_world.launch
    ```

2. On another terminal run the rviz for this world, in order to navigate the robot through it:
    ```
    roslaunch turtlebot_rviz_launchers view_navigation.launch
    ```

3. You should also execute the amcl, because the pose of the robot is fundamental for this application (don't forget to specify your map file):
    ```
    roslaunch turtlebot_gazebo amcl_demo.launch map_file:=<absolute-path-name>.yaml
    ```

4. Finally run the *robot_treasure_hunting* application:
    ```
    roslaunch robot_treasure_hunting robo_treasure.launch
    ```

5. Go to rviz and Add the Marker that publishes to the */treasure_viz/treasure_marker* topic.

6. Then, after selecting the missing object, navigate the robot via rviz and ... Enjoy!