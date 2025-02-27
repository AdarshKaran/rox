# **rox**

This package provides provides the bringup, robot description and navigation files for the latest `rox` platform supporting UR10, UR10e, UR5, UR5e and Elite EC66 arms.

## **Launch Command**

To start the simulation:
```sh
ros2 launch rox_bringup bringup_sim_launch.py arm_type:=ur10
```

## **Launch Arguments**

To check available arguments:
```sh
ros2 launch rox_bringup bringup_sim_launch.py --show-args
```

### **Arguments**
```text
'imu_enable':
    Enable IMU - Options: True/False
    (default: 'False')

'd435_enable':
    Enable Realsense - Options: True/False
    (default: 'False')

'arm_type':
    Arm Types:
        Elite Arms: ec66, cs66
        Universal Robotics (UR): ur5, ur10, ur5e, ur10e
    (default: '')

'frame_type':
    Frame type - Options: short/long
    (default: 'short')

'rox_type':
    Robot type - Options: argo/diff/trike/meca
    (default: 'argo')

'use_ur_dc':
    Set this argument to True if you have an UR arm with DC variant
    (default: 'false')

'initial_joint_controller':
    Robot controller to start:
        Elite Arms: arm_controller
        Universal Robotics (UR): joint_trajectory_controller, scaled_joint_trajectory_controller
```

## **Note**
For simulation, set:
```yaml
speed_scaling_interface_name: ""
```
This setting is commented in every UR arm `ur_controllers.yaml` file under `rox_bringup/configs/ur/`.

## **Navigation Commands**

Start navigation:
```sh
ros2 launch rox_navigation navigation.launch.py rox_type:=argo use_sim_time:=True use_rviz:=true use_amcl:=False
```

## **MoveIt2 Simulation**

Start MoveIt2 with Gazebo:
```sh
ros2 launch neo_rox_moveit2 neo_ur_moveit.launch.py arm_type:=ur10 use_sim_time:=True prefix:=ur10 launch_rviz:=True use_gz:=true
```

---

## **Changelog**

### **[Date: 2025-02-27]**

#### **rox_navigation**

- Updated the navigation launch by adding an argument to launch rviz with no outputs in the current terminal Issue #51
- Added initial pose to nav omni and diff params file, updated model type

### **[Date: 2025-02-26]**

#### **rox_description**

- Cannot update ur_arm.xacro to conditionally include ur_robot_driver only for real robot since needed since gz sim also uses the same ur_ros2_control xacro macro from ur_robot_driver pkg.
- Removed neo_gz_worlds and rox_description dependencies from rox_bringup package.xml.

#### **rox_bringup**

- Conditionally added elite_description to the environment variable only if an Elite arm is in use-> in bringup_sim_launch.py. Tested the same.
---
### **[Date: 2025-02-14]**

#### **rox_description**


- Resolved movement issues in Argo drive in Gazebo where it did not respond to teleop velocities lower than 0.03 m/s → Issue #47.
- Adjusted the positions of various robot components in the URDF to align with the mechanical documentation.
- Added dynamic properties to wheels and joints for more accurate simulation.
- Fine-tuned those dynamic properties.
- Fixed stability issues with the robot when the arm is mounted.
- Thoroughly tested the /odom and /cmd_vel topics to ensure the robot responds correctly to the given velocities.
- Refactored URDF structure to accommodate the above changes.
- Documented updates in CHANGELOG.

To run and test the changes:
```sh
ros2 launch rox_bringup bringup_sim_launch.py rox_type:=argo arm_type:=ur10
```
rox_type options: argo, diff, trike

---

### **[Date: 2025-02-04]**

#### **rox_description**
- Updated `gazebo.xacro` for migration to Modern Gazebo (Ionic).
- Added modular URDF xacros for `ur_arm` and `elite_arm`.
- Refactored `rox.urdf.xacro` to be modular.

#### **rox_bringup**
- Added ROS 2 Control and Joint Trajectory Controller configurations for UR and Elite arms.
- Updated `gz_bridge_config.yaml` to support the Modern Gazebo migration and updated /cmd_vel message type.
- Modified `bringup_sim_launch.py` to accommodate the new URDF format and include necessary ROS 2 Control nodes for arms.
- Updated the teleop publish message type for /cmd_vel topic.
- Added model paths to `GZ_SIM_RESOURCE_PATH` env variable in launch file.
- Set use ac/dc parameter in simulation launch file and updated arm position(height) on cabinet for ac variant.
- UR arm urdf in `ur_description` package for rolling is different from the iron distro. So this package was adapted to those changes and appropriate packages were used.

#### **General**
- Updated dependencies.
- Packages restructuring.
