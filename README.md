Fairino ROS2 Driver (Version 3.7.8)
This document provides a quick tutorial for using MoveIt2 with Fairino Robots, compatible with web version 3.7.8. For a detailed guide, refer to the official documentation: Fairino ROS2 Guide.
Checking the Robot Web Version
To verify the web version on your robot:

Open the Fairino Web App.
Navigate to System > About.
Confirm that the web version is 3.7.8. If it differs, follow the steps below to update.

Updating the Web Version
To change the web version to 3.7.8:

Download the software package from Fairino Robot Software:
Select FAIRINO-CobotSoftware-QX-V3.7.8-Release-250120.
Unzip the folder to your file system.


In the Web App, go to Application > Tool App > System Upgrade.
In the Software Upgrade section, click Choose File and select software.tar.gz from the unzipped folder.
Click Upload and wait for the Web App to prompt you to restart the control box.
After restarting, verify the web version in System > About.

Setting Up the ROS2 Workspace
Follow these steps to set up your ROS2 environment and integrate the Fairino ROS2 Driver:

Prepare the Environment:

Ensure you have Ubuntu 22.04 with ROS2 Humble installed. Refer to the ROS2 Setup Guide for detailed instructions.


Create a ROS2 Workspace:
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws


Download the Driver:

Download and unzip the contents of the Fairino ROS2 Driver repository into the ~/ros2_ws/src directory.


Build the Workspace:

To build all packages:colcon build
source install/setup.bash


To build specific packages, use the following commands:
fairino_msgs:colcon build --packages-select fairino_msgs
source install/setup.bash


fairino_hardware:colcon build --packages-select fairino_hardware
source install/setup.bash


fairino_description:colcon build --packages-select fairino_description
source install/setup.bash


fairino5_v6_moveit2_config (example MoveIt2 configuration):colcon build --packages-select fairino5_v6_moveit2_config
source install/setup.bash






Custom MoveIt2 Package (Optional):

To create a customized MoveIt2 package, follow the MoveIt2 Configuration Guide.


Launch the Demo:

For the default package (e.g., FR3):ros2 launch fairino3_v6_moveit2_config demo.launch.py


For a customized MoveIt2 package (e.g., FR3):ros2 launch fairino3_v6_robot_moveit_config demo.launch.py



After launching, the robot should appear in the RViz environment in its packing position. You can:

Set Target Position: Drag and drop the blue sphere at the robot's end effector in the 3D interface (right side).
Adjust End Effector Attitude: Use the red, green, and blue rings to rotate the end effector.
Plan Trajectory: Click the Plan button on the left to generate a trajectory.
Execute Movement: Click the Execute button to move the robot along the planned trajectory.
Plan & Execute: Use the Plan & Execute button to automatically plan and execute the trajectory.
Adjust Joint Angles: Switch to the Joints tab to modify joint angles, then use the Plan, Execute, or Plan & Execute buttons to move the robot.


Fairino Hardware Compilation:

Compile the fairino_hardware plugin package as described above. Upon successful compilation, the file libfairino_hardware.so will be generated in ~/ros2_ws/install/fairino_hardware/lib/fairino_hardware.
Edit the ROS2 control configuration file:
Open ~/ros2_ws/install/fairino3_v6_moveit2_config/share/fairino3_v6_moveit2_config/config/fairino3_v6_robot.ros2_control.xacro.
Modify line 9 as shown in the referenced image: Configuration Image.


Re-run the demo launch file:source install/setup.bash
ros2 launch fairino3_v6_moveit2_config demo.launch.py



The robot's actual position should now be reflected in RViz, enabling control via MoveIt2 and RViz.


