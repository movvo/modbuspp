cmake_minimum_required(VERSION 3.5)
project(modbuspp)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

find_package(ament_cmake REQUIRED)
find_package(rclcpp)

set(dependencies
  rclcpp
)

include_directories(
    include
)

## Declare a cpp library for just Ethernet/IP generic stuff
add_library(${PROJECT_NAME} SHARED
  "src/modbus.cpp"
)

ament_target_dependencies(${PROJECT_NAME} 
                          ${dependencies})

## Mark executables and libraries for installation
install(DIRECTORY include/
  DESTINATION include/
)

install(TARGETS
  ${PROJECT_NAME}
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

ament_export_include_directories(include)
ament_export_libraries(${PROJECT_NAME})
ament_export_dependencies(${dependencies})

ament_package()