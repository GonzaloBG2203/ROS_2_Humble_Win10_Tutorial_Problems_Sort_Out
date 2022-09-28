# ROS_2_Humble_Win10_Tutorial_Problems_Sort_Out

Sort out of common errors that appear while running the ROS 2 Humble Tutorials and configuring its environment in Windows 10. As a newbie programmer I followed this tutorial for Windows, before knowing that Linux is the way to go in programming. If anybody goes ahead and follows the Windows tutorial, here are the common errors and difficulties I encountered. These are **MY** solutions (they worked for me, but they might be wrong), I know very little about programming and the solutions I found were a resut of Internet research. Please, feel free to alter these solutions if you have more experience and see that something is wrong. 

Thanks for reading!

Web: https://docs.ros.org/en/humble/Tutorials.html

## You can view all of a node’s current parameter values by using the command:


    ros2 param dump <node_name>


The command prints to the standard output (stdout) by default but you can also redirect the parameter values into a file to save them for later. To save your current configuration of /turtlesim’s parameters into the file turtlesim.yaml, enter the command:

    ros2 param dump /turtlesim > turtlesim.yaml


You will find a new file in the working directory your shell is running in **(IN MY CASE, C:\DEV\ROS2_HUMBLE. IT´S THE DIRECTORY YOUR ROS 2 PROGRAM IS STORED IN. THE FILE IS CALLED TURTLESIM.YAML)** . If you open this file, you’ll see the following content:

- /turtlesim:
    - ros__parameters:
      - background_b: 255
      - background_g: 86
      - background_r: 150
       - qos_overrides:
         - /parameter_events:
           - publisher:
             - depth: 1000
             - durability: volatile
             - history: keep_last
             - reliability: reliable
          - use_sim_time: false
    
   **YOU CAN EDIT THESE COLOR VALUES (RGB, 0-255) IN YOUR IDE (VISUAL STUDIO), SAVE THE CHANGES, RUN THE COMMAND "ROS2 PARAM LOAD /TURTLESIM TURTLESIM.YAML" AND WATCH THE BACKGROUND CHANGE COLOUR!**

## Now let’s send an action goal from the command line with the following syntax:

    ros2 action send_goal <action_name> <action_type> <values>

  *<values> need to be in YAML format. (https://www.cloudbees.com/blog/yaml-tutorial-everything-you-need-get-started)

Keep an eye on the turtlesim window, and enter the following command into your terminal:

    ros2 action send_goal /turtle1/rotate_absolute turtlesim/action/RotateAbsolute "{theta: 1.57}"

Tasks

 Running a Launch File

  Open a new terminal and run:

        ros2 launch turtlesim multisim.launch.py

  ERROR: Failed to load entry point 'launch': No module named 'lark'...**EXECUTE: "PIP3 INSTALL LARK" IN YOUR TERMINAL. FOR OTHER ERRORS LIKE THIS (NO MODULE NAMED "...", USE THE COMMAND: "PIP3 INSTALL ...", AS A WAY TO INSTALL MISSING PYTHON MODULES.**

## Recording and playing back data 3 ros2 bag record:
To record the data published to a topic use the command syntax:

        ros2 bag record <topic_name>

Before running this command on your chosen topic, open a new terminal and move into the bag_files directory you created earlier, because the rosbag file will save in the directory where you run it.

Run the command:

    ros2 bag record /turtle1/cmd_vel

**ERROR!** 
- Failed to load entry point 'record': DLL load failed while importing _reader: The specified module could not be found.
    - Traceback (most recent call last):
        - File "C:\dev\ros2_humble\Scripts\ros2-script.py", line 33, in <module>
    sys.exit(load_entry_point('ros2cli==0.18.3', 'console_scripts', 'ros2')())
        - File "C:\dev\ros2_humble\Lib\site-packages\ros2cli\cli.py", line 50, in main
    add_subparsers_on_demand(
        - File "C:\dev\ros2_humble\Lib\site-packages\ros2cli\command\__init__.py", line 250, in add_subparsers_on_demand
    extension.add_arguments(
        - File "C:\dev\ros2_humble\Lib\site-packages\ros2bag\command\bag.py", line 26, in add_arguments
    add_subparsers_on_demand(
        - File "C:\dev\ros2_humble\Lib\site-packages\ros2cli\command\__init__.py", line 237, in add_subparsers_on_demand
    extension = command_extensions[name]
- KeyError: 'record'

  **SOLUTION:**(this one was hard to get, based on https://docs.ros.org/en/rolling/How-To-Guides/Installation-Troubleshooting.html)

 1. Download Dependencies: https://github.com/lucasg/Dependencies/releases/download/v1.11.1/Dependencies_x64_Release.zip
 2. Unzip and run DependenciesGui (double click).
 3. Drag to the new window that opens from DependenciesGui C:\dev\ros2_humble\Lib\site-packages\rosbag2_py\_reader.cp38-win_amd64  (Python Extension Module).
 4. Find in the left list  the .dll that is missing. (In my case, tinyxml2.dll).
 5. Use the Windows search utility to find the missing .dll (In my case, it was in C:\ProgramData\chocolatey\lib\tinyxml2\lib\).
 6. Copy the missing .dll and paste it in the folder where _reader.cp38-win_amd64 is (In my case C:\dev\ros2_humble\Lib\site-packages\rosbag2_py\)


## ADD SOME SOURCES (using colcom to build packages)
**Command** “git clone https://github.com/ros2/examples src/examples -b humble” **returns error:**
“'git' is not recognized as an internal or external command, operable program or batch file.”

**GO TO** https://github.com/ros2/examples **AND DOWNLOAD THE PACKAGE. RIGHT UPPER CORNER, GREEN BUTTON “CODE”, DOWNLOAD ZIP. UNZIP. CREATE FOLDER “EXAMPLES” IN C:\dev\ros2_ws\src\ (WHERE YOU HAVE YOUR SRC FOLDER). COPY THE UNZIPPED FILES/FOLDERS:** 
- CONTRIBUTING.md
- LICENSE
- rclcpp
- rclpy
- README.md


## Build the workspace:

**EXECUTING THIS COMMAND** “colcon build --symlink-install --merge-install” **GIVES A BUNCH OF ERRORS, THE LAST ONE BEING:** “VisualStudioVersion is not set, please run within a Visual Studio Command Prompt”. **INSTALL ***VISUAL STUDIO CODE***, IT HAS A VISUAL STUDIO COMMAND PROMPT INCLUDED (I HAD VISUAL STUDIO "SIMPLE VERSION", I COULDN´T START A COMMAND PROMPT FROM THE SOFTWARE).**

