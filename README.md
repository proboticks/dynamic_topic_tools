# dynamic_topic_tools
A topic throttler with dynamic configuration of throttling parameters using ROS service calls. 
<br>
Forked from https://github.com/ros/ros_comm/blob/noetic-devel/tools/topic_tools/src/throttle.cpp

# Changes from ros_comm/topic_tools:
- Nodes are no longer anonymous; node name is set to the topic name suffixed with "_throttler"
- Created Services **set_param** anf **get_param** to set and get throttling parameters
- Services set/get 4 parameters:
  - messages_mode: True if MESSAGE mode, False if BYTES mode
  - msgs_per_sec: Maximum messages per second to let through (For MESSAGE mode)
  - bytes_per_sec: Maximum bytes per second to let through  (For BYTES mode)
  - sampling_window: Window (in seconds) over which to sample (For BYTES mode)
- Added a global varibale (g_msgs_per_sec) to track maximum messages per second for retreival using **get_params**

## Command line example
### Start a topic:
```
rostopic pub -r 10 /cmd_vel geometry_msgs/Pose2D '{x: 0.1, y: 0.2, theta: 3.0}'
```

### Start a throttler in BYTES mode
```
rosrun dynamic_topic_tools throttle bytes test_pose 1024 1.0
```

### Set Params
```
rosservice call /test_pose_throttler/set_params "messages_mode: false
bytes_per_sec: 10
msgs_per_sec: 0
sampling_window: 1.0"
```

### Get Params
```
rosservice call /test_pose_throttler/get_params
```