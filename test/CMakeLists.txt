cmake_minimum_required(VERSION 3.0)

set(CMAKE_CXX_FLAGS "-std=c++14 ${CMAKE_CXX_FLAGS} -Wl,-wrap,udev_monitor_enable_receiving,-wrap,udev_monitor_get_fd,-wrap,udev_monitor_new_from_netlink,-wrap,udev_device_get_is_initialized")

enable_testing()


add_executable(monitor_test monitor_test.cpp)
add_executable(device_test device_test.cpp)
target_link_libraries(monitor_test udevpp pthread gtest gtest_main)
target_link_libraries(device_test udevpp pthread gtest gtest_main )

add_test(MonitorTest monitor_test)
add_test(DeviceTest device_test)


# Set up a target for 'make check' if needed
if(NOT TARGET check)
  add_custom_target(check COMMAND ${CMAKE_CTEST_COMMAND} )
endif()

#force the 'check' target to depend on the test executables, so that we have a target that will build them in parent projects.
add_dependencies(check monitor_test)
add_dependencies(check device_test)

