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
