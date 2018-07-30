cmake_minimum_required(VERSION 2.8.3)
project(custom_msgs)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation
  geometry_msgs
)

add_message_files(
  FILES
  Form.msg
  Obstacles.msg
  Zone.msg
)

generate_messages(
  DEPENDENCIES
  std_msgs
  geometry_msgs
)

catkin_package(
 	CATKIN_DEPENDS roscpp rospy message_runtime std_msgs geometry_msgs
 )

include_directories(
  ${catkin_INCLUDE_DIRS}
)
