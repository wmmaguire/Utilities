cmake_minimum_required(VERSION 3.8)
# project name
project(cpp_visualization)
set(CMAKE_CXX_STANDARD 11)
# define executable path
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU" OR
		"${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
	set(warnings "-Wall -Wextra -Werror")
endif()

find_package(PythonLibs 2.7)
# path to project header

include_directories(matplotlib-cpp)
include_directories(/usr/local/include/python2.7)

INSTALL (
    DIRECTORY matplotlib-cpp/
    DESTINATION include/python2.7/
    FILES_MATCHING PATTERN "*.h*")

#target_include_directories(cpp_visualization PRIVATE ${PYTHON_INCLUDE_DIRS})
# adds lib to sys env
# add_library(matplotlibcpp SHARED matplotlib-cpp/matplotlibcpp.h)

# define source files
# explicit
#set(SOURCES
	#${CMAKE_CURRENT_SOURCE_DIR}/src/lib_test.cpp
	#)
# implicit - global
file(GLOB SOURCES "matplotlib-cpp/*.cpp")

set(EXAMPLES_SRC
	${CMAKE_CURRENT_SOURCE_DIR}/matplotlib-cpp/examples
)

add_executable(minimal matplotlib-cpp/examples/minimal.cpp)
target_link_libraries(minimal ${PYTHON_LIBRARIES})
