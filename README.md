# Gazebo Gripper Action Controller

The `gazebo_gripper_action_controller` is a ROS control gripper action controller designed for Gazebo simulation environments. This controller has been derived from the original [ros_controllers](https://github.com/ros-controls/ros_controllers) repository with specific modifications to enhance its functionality.

<img src="media/gazebo.gif" alt="App GIF">

## Features

- The stalling detection mechanism has been improved. Instead of relying on stall velocity thresholds, this version uses a position threshold approach. This provides better reliability since velocity data can be noisier.
- The traditional behavior of the controller, which caused actions to fail upon stalling, has been adjusted. Now, actions will succeed when stalling occurs, making it more convenient for picking objects in MoveIt.

## How to Use in `ros_control`

To integrate the GazeboGripperActionController into your `ros_control` configuration, follow these steps:

1. Navigate to your controller config yaml file. If you use `moveit_setup_assistant`, this would be in `<your_moveit_config_pkg>/config/gazebo_controllers.yaml`.

```yaml
gripper_controller:                                        # Your controller name
  type: position_controllers/GazeboGripperActionController # Name of the controller type
  joint: finger_joint                                      # The joint you are controlling
  goal_tolerance: 0.1                                      # Goal tolerance in radians
  stall_position_threshold: 0.05 # Tune to fit your robot  # Arm is stalling if position (radians) hasn't moved over the threshold
  stall_timeout: 0.5                                       # Arm has stalled if timeout (seconds) is reached
  action_monitor_rate: 10                                  # Frequency (in Hz) at which the action goal status is monitored
```
