# http://ros.org/doc/groovy/api/catkin/html/user_guide/supposed.html
cmake_minimum_required(VERSION 2.8.3)
project(ros_ethercat_model)

# Load catkin and all dependencies required for this package
find_package(catkin REQUIRED COMPONENTS 
    roscpp
    hardware_interface
    pluginlib
    urdf
    kdl_parser
    pr2_mechanism_msgs
)

find_package(Boost REQUIRED COMPONENTS system thread)
include_directories(include ${Boost_INCLUDE_DIRS} ${catkin_INCLUDE_DIRS})

catkin_package(
DEPENDS
    tinyxml
    urdfdom
CATKIN_DEPENDS
    roscpp
    hardware_interface
    pluginlib
    urdf
    kdl_parser
    pr2_mechanism_msgs
INCLUDE_DIRS
    include
LIBRARIES
    ${PROJECT_NAME}
)

add_definitions(-O3)

add_library(${PROJECT_NAME}
    src/robot.cpp
)

target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES} )
add_dependencies(${PROJECT_NAME} ${catkin_EXPORTED_TARGETS})

install(TARGETS ${PROJECT_NAME}
   RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)
install(DIRECTORY include/${PROJECT_NAME}/
   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
)