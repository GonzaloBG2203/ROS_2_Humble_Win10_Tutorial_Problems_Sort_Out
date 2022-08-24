# ROS-2-Humble-Tutorial-Problems-Sort-Out
Sort out of common errors that appear while running the ROS 2 Humble Tutorials and configuring its environment.
Web: https://docs.ros.org/en/humble/Tutorials.html

5 ros2 param dump
You can view all of a node’s current parameter values by using the command:

ros2 param dump <node_name>
The command prints to the standard output (stdout) by default but you can also redirect the parameter values into a file to save them for later. To save your current configuration of /turtlesim’s parameters into the file turtlesim.yaml, enter the command:

ros2 param dump /turtlesim > turtlesim.yaml
You will find a new file in the working directory your shell is running in **(IN MY CASE, C:\DEV\ROS2_HUMBLE. IT´S THE DIRECTORY YOUR ROS 2 PROGRAM IS STORED IN. THE FILE IS CALLED TURTLESIM.YAML)** . If you open this file, you’ll see the following content:

/turtlesim:
  ros__parameters:
    background_b: 255
    background_g: 86
    background_r: 150
    qos_overrides:
      /parameter_events:
        publisher:
          depth: 1000
          durability: volatile
          history: keep_last
          reliability: reliable
    use_sim_time: false
    
   **YOU CAN EDIT THESE COLOR VALUES IN YOUR IDE (I HAVE VISUAL STUDIO), SAVE THE CHANGES, RUN THE COMMAND "ROS2 PARAM LOAD /TURTLESIM TURTLESIM.YAML" AND WATCH THE BACKGROUND CHANGE COLOUR!**
Now let’s send an action goal from the command line with the following syntax:

ros2 action send_goal <action_name> <action_type> <values>
<values> need to be in YAML format. **(https://www.cloudbees.com/blog/yaml-tutorial-everything-you-need-get-started)**

Keep an eye on the turtlesim window, and enter the following command into your terminal:

ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: 1.57}"
