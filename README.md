# rox

### Launch Command

To see the simulation arguments, use the following command:

`ros2 launch rox_bringup bringup_sim_launch.py --show-args`

```
Arguments (pass arguments as '<name>:=<value>'):

    'imu_enable':
        Enable IMU - Options: True/False
        (default: 'False')

    'd435_enable':
        Enable Realsense - Options: True/False
        (default: 'False')

    'arm_type':
        Arm used in the robot:
	 currently only the following Universal Robotics arms are supported
	 (ur5, ur10, ur5e, ur10e)
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
```

## Simulating the rox Robot with a UR Arm

To simulate the rox robot with a Universal Robotics (UR) arm, you need to set the `arm_type` parameter. Below is an example of how to launch the simulation with the `ur10` arm type

`ros2 launch rox_bringup bringup_sim_launch.py arm_type:=ur10`