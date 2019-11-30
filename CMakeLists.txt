cmake_minimum_required(VERSION 3.13.4)

project("HelloWorld")

# PROJECT_NAME now == "HelloWord", the value set in the project command
# Dereference the variable to get its value "${PROJECT_NAME}"
# Best to surround that with "" for string values, as it could
# contain spaces and CMake uses spaces as its delimiter.

# The add_executable command has two parameters:
# the first names the executable.  Here, we use the project name.
# the second names the source files needed to build it.
add_executable("${PROJECT_NAME}" main.cpp)

# The install command installs the executable you name in the 1st
# parameter to the destination in the 2nd.  Here, bin, is relative
# to ${CMAKE_INSTALL_PREFIX}.  So, the full path in our example
# would be ${CMAKE_INSTALL_PREFIX}/bin
# On my linux box, ${CMAKE_INSTALL_PREFIX} defaults to /usr/local
install(TARGETS "${PROJECT_NAME}" DESTINATION bin)
install(FILES "main.cpp" DESTINATION src)

# If you use cmake-gui, you can see the CMake cache variables.
# CMake cache variables are used to customize your build.

# This next line is required to work with CDash.  (so is the include(CTest) line)
enable_testing()
# To use CTest, you need to include it:
include(CTest)

# ${CMAKE_CURRENT_BINARY_DIR} points to the build directory.
add_test("test1" "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}")
