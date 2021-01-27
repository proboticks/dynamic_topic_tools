# dynamic_topic_tools
A topic throller with dynamic configuration of throlling parameters using service calls.
Forked from https://github.com/ros/ros_comm/blob/noetic-devel/tools/topic_tools/src/throttle.cpp


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