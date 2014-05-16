cmake_minimum_required(VERSION 2.8.3)
project(vrep_plugin)

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#Declare build dependencies
find_package(catkin REQUIRED 
    COMPONENTS
    roscpp
    std_msgs
    sensor_msgs
    vrep_common
    image_transport
    tf
)

##Needed for ros packages
catkin_package(CATKIN_DEPENDS roscpp std_msgs sensor_msgs vrep_common image_transport tf
		LIBRARIES v_repExtRos)

include_directories( include
    ${catkin_INCLUDE_DIRS})

add_library(v_repExtRos src/vrep_plugin.cpp src/v_repLib.cpp src/ROS_server.cpp src/vrepSubscriber.cpp) 
target_link_libraries(v_repExtRos pthread ${catkin_LIBRARIES})
target_link_libraries(v_repExtRos dl ${catkin_LIBRARIES})
