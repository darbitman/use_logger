cmake_minimum_required(VERSION 3.10)

project(UseLogger VERSION 0.0.1 LANGUAGES CXX)

set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)

# Link this "library" to set the c++ standard/compile-time options
add_library(project_options INTERFACE)
target_compile_features(project_options INTERFACE cxx_std_17)

# Link this "library" to use warnings
add_library(project_warnings INTERFACE)
include(cmake/CompilerWarnings.cmake)
set_project_warnings(project_warnings)

## One way is to use TARGETS and link CONAN_PKG::logger
include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup(TARGETS)
add_executable(main main.cpp)
target_link_libraries(main PRIVATE CONAN_PKG::logger
                      $<BUILD_INTERFACE:project_options>
                      $<BUILD_INTERFACE:project_warnings>)


## other option is not to use TARGETS
# include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
# conan_basic_setup()
# add_executable(main main.cpp)
# target_link_libraries(main PRIVATE logger
#                       $<BUILD_INTERFACE:project_options>
#                       $<BUILD_INTERFACE:project_warnings>)
