cmake_minimum_required(VERSION 2.8.3)
project(robot_treasure_area)



set(CMAKE_CXX_FLAGS "-std=c++11 -O2")

find_package(catkin REQUIRED COMPONENTS
  rospy
  roslib
  std_msgs
  sensor_msgs
  message_generation
)

find_package(Boost 1.40 COMPONENTS program_options REQUIRED)

add_service_files(
    FILES
    ObjectChoice.srv
)

add_message_files(
  FILES
  RadiusMsg.msg
)

generate_messages(
	DEPENDENCIES
        sensor_msgs
	std_msgs
)

catkin_package(
   	LIBRARIES ${PROJECT_NAME}
  	CATKIN_DEPENDS roslib std_msgs
)

include_directories(${catkin_INCLUDE_DIRS} src)

aux_source_directory(src SRC_LIST)

file(GLOB_RECURSE  LIB_CPP "./src/*.cpp")
file(GLOB_RECURSE  LIB_C "./src/*.c")
file(GLOB_RECURSE  LIB_HDRS "./src/*.h")
 
