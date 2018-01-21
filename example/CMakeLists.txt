
if(TARGET udevpp)
  add_library(udevpp::udevpp ALIAS udevpp)
else()
  # Add NO_CMAKE_BUILDS_PATH for windows if using CMake-GUI to build packages
  # to avoid searching in temporary build directory of Foo project
  # See 5:
  #    * http://www.cmake.org/cmake/help/v3.0/command/find_package.html
  find_package(udevpp CONFIG REQUIRED)
endif()

# Define an executable
add_executable(enumerate
    src/enumerate.cpp)
    
add_executable(led_flash
    src/ledflash.cpp)

# Define the libraries this project depends upon
target_link_libraries(enumerate udevpp)

# Define the libraries this project depends upon
target_link_libraries(led_flash udevpp)
