# gazebo_gripper_action_controller
ROS control gripper action controller for Gazebo. Modified from https://github.com/ros-controls/ros_controllers. Changes stall velocity threshold to use position threshold. Actions now will succeed on stalling instead of failing.
### How to use in moveit_config:
---
* In gazebo_controllers.yaml, add the following:
  ```
  gripper_controller:
    type: position_controllers/GazeboGripperActionController # Name of controller type
    joint: finger_joint                                      # The joint you are controlling
    goal_tolerance: 0.1                                      # Goal tolerance in radians
    stall_position_threshold: 0.05 # Tune to fit your robot  # Arm is stalling if position (radians) hasn't moved over threshold
    stall_timeout: 0.5                                       # Arm has stalled if timeout (sec) reached
    action_monitor_rate: 10                                  # Frequency (in Hz) at which the action goal status is monitored
  ```
