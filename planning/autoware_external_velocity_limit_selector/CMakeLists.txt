cmake_minimum_required(VERSION 3.14)
project(autoware_external_velocity_limit_selector)

find_package(autoware_cmake REQUIRED)
autoware_package()

generate_parameter_library(external_velocity_limit_selector_parameters
  param/external_velocity_limit_selector_parameters.yaml
)

ament_auto_add_library(external_velocity_limit_selector_node SHARED
  src/external_velocity_limit_selector_node.cpp
)

target_link_libraries(external_velocity_limit_selector_node
  external_velocity_limit_selector_parameters
)

rclcpp_components_register_node(external_velocity_limit_selector_node
  PLUGIN "autoware::external_velocity_limit_selector::ExternalVelocityLimitSelectorNode"
  EXECUTABLE external_velocity_limit_selector
)

if(BUILD_TESTING)
  add_launch_test(
    test/test_external_velocity_limit_selector_node_launch.py
    TIMEOUT "30"
  )
endif()

ament_auto_package(INSTALL_TO_SHARE
  launch
  config
)
