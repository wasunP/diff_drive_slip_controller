cmake_minimum_required(VERSION 2.8.3)
project(diff_drive_slip_controller)

find_package(catkin REQUIRED COMPONENTS
    controller_interface
 #   dynamic_reconfigure
    nav_msgs
    realtime_tools
    tf
    urdf
)

#generate_dynamic_reconfigure_options(cfg/DiffDriveController.cfg)

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES ${PROJECT_NAME}
)

include_directories(
  include
)

include_directories(SYSTEM
  ${catkin_INCLUDE_DIRS}
)

add_library(${PROJECT_NAME} src/diff_drive_slip_controller.cpp src/odometry.cpp src/speed_limiter.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES})
#add_dependencies(${PROJECT_NAME} ${${PROJECT_NAME}_EXPORTED_TARGETS} ${PROJECT_NAME}_gencfg)

install(DIRECTORY include/${PROJECT_NAME}/
        DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION})

install(TARGETS ${PROJECT_NAME}
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
  )

install(FILES diff_drive_slip_controller_plugins.xml
    DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION})
