cmake_minimum_required(VERSION 2.8.3)
project(dynamic_topic_tools)

## Compile as C++11, supported in ROS Kinetic and newer
set(CMAKE_CXX_FLAGS "-std=c++11 ${CMAKE_CXX_FLAGS}")

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation
  topic_tools
)

find_package(OpenCV REQUIRED
  COMPONENTS
  CONFIG
)


###################################
## catkin specific configuration ##
###################################
include_directories(
  include
  ${catkin_INCLUDE_DIRS}
)

add_service_files(
  FILES
  SetThrottleParams.srv
  GetThrottleParams.srv
)


generate_messages(
  DEPENDENCIES
  std_msgs
)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES sim_builder
  CATKIN_DEPENDS std_msgs message_runtime
)

###########
## Build ##
###########
add_executable(
  throttle
  src/throttle.cpp
)

add_dependencies(throttle dynamic_topic_tools_generate_messages_cpp)

target_link_libraries(throttle
  ${catkin_LIBRARIES}
  ${PCL_LIBRARIES}
  ${Boost_LIBRARIES}
  ${Eigen_LIBRARIES}
)
