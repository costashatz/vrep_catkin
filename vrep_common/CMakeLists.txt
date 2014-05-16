cmake_minimum_required(VERSION 2.8.3)
project(vrep_common)

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#List to make rest of code more readable
set( MESSAGE_DEPENDENCIES
    std_msgs
    sensor_msgs
)

#Declare build dependencies
find_package(catkin REQUIRED 
    COMPONENTS
    message_generation
    ${MESSAGE_DEPENDENCIES} )


file(GLOB MSGS RELATIVE msg msg/*.msg)
file(GLOB SRVS RELATIVE srv srv/*.srv)

add_message_files(DIRECTORY msg
	${MSGS}
)

add_service_files(DIRECTORY srv
	${SRVS}
)

#And now generate the messages
generate_messages(DEPENDENCIES ${MESSAGE_DEPENDENCIES})

#Declare package run-time dependencies
catkin_package( CATKIN_DEPENDS message_runtime ${MESSAGE_DEPENDENCIES})
