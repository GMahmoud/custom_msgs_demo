# ##############################################################################
# Version setup
# ##############################################################################

set(PACKAGE_NAME custom_msgs)
file(STRINGS ${CMAKE_CURRENT_LIST_DIR}/VERSION PROJECT_VERSION)
message(STATUS "Project version: ${PROJECT_VERSION}")

# ##############################################################################
# Project information
# ##############################################################################

cmake_minimum_required(VERSION 3.5.1)
project(${PACKAGE_NAME} LANGUAGES C CXX VERSION ${PROJECT_VERSION})
set(PROJECT_RELEASE_TYPE release) # alpha, beta, release

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/cmake_modules")
include(declarations)

# ##############################################################################
# Load and setup packages
# ##############################################################################

find_package(catkin REQUIRED
             COMPONENTS roscpp
                        rospy
                        std_msgs
                        message_generation
                        geometry_msgs
                        nav_msgs)

# ##############################################################################
# Generate messages and configurations
# ##############################################################################

add_message_files(DIRECTORY
                  msg/state_machine
                  FILES
                  State.msg
                  Transition.msg
                  MachineDescription.msg)

add_message_files(DIRECTORY
                  msg/detection
                  FILES
                  FaceInfo.msg
                  DetectedFaces.msg
                  NormalizedFaces.msg)

add_message_files(DIRECTORY
                  msg/display
                  FILES
                  TextCmd.msg)

add_message_files(DIRECTORY
                  msg/virtual_layer
                  FILES
                  Form.msg
                  Obstacles.msg
                  Zone.msg)

add_message_files(DIRECTORY
                  msg/supervisor
                  FILES
                  AppCmd.msg
                  Dependency.msg
                  Service.msg
                  Process.msg)

add_message_files(DIRECTORY
                  msg/nav
                  FILES
                  Map64.msg)

add_message_files(DIRECTORY
                  msg/image
                  FILES
                  Image64.msg)

add_message_files(DIRECTORY
                  msg/control
                  FILES
                  HeadCmd.msg
                  HeadPose.msg
                  PhoneCmdVel.msg)

add_message_files(DIRECTORY
                  msg/alpha1s
                  FILES
                  BatteryState.msg)

add_message_files(DIRECTORY
                  msg/hardware
                  FILES
                  ColorRGB.msg
                  Leds.msg)

add_message_files(DIRECTORY
                  msg/create
                  FILES
                  Bumper.msg
                  ChargingState.msg
                  Mode.msg
                  DefineSong.msg
                  PlaySong.msg)

add_message_files(DIRECTORY
                  msg/rtc
                  FILES
                  MessageRTC.msg)

add_message_files(DIRECTORY
                  msg/console
                  FILES
                  Log.msg)

add_message_files(DIRECTORY
                  msg/monitoring
                  FILES
                  Info.msg)

add_message_files(DIRECTORY
                  msg/ssh
                  FILES
                  Heartbeat.msg)
# For Arduino
add_message_files(DIRECTORY
                  msg
                  FILES
                  LedRGBColors.msg
                  Battery.msg)

generate_messages(DEPENDENCIES
                  std_msgs
                  geometry_msgs
                  nav_msgs)

# ##############################################################################
# Setup catkin packages
# ##############################################################################

catkin_package(CATKIN_DEPENDS
               roscpp
               rospy
               message_runtime
               std_msgs
               geometry_msgs
               nav_msgs)
