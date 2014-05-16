cmake_minimum_required(VERSION 2.8.3)
project(vrep_joy)

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#Declare build dependencies
find_package(catkin REQUIRED 
    COMPONENTS
    roscpp
    joy
)

##Needed for ros packages
catkin_package(CATKIN_DEPENDS roscpp joy)

add_executable(vrep_joy src/vrep_joy.cpp)
target_link_libraries(vrep_joy
    ${catkin_LIBRARIES}
    ${NAOqi_LIBRARIES}
    ${Boost_LIBRARIES})
add_dependencies(vrep_joy ${catkin_EXPORTED_TARGETS})
