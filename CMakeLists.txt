cmake_minimum_required(VERSION 3.8.2)

# Pre-enviroments set
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_VERBOSE_MAKEFILE ON)
SET(CMAKE_BUILD_TYPE "Debug") 
SET(CMAKE_CXX_FLAGS_DEBUG "$ENV{CXXFLAGS} -O0 -Wall -g -ggdb")
SET(CMAKE_CXX_FLAGS_RELEASE "$ENV{CXXFLAGS} -O3 -Wall")
SET(CMAKE_EXPORT_COMPILE_COMMANDS ON)

if(CMAKE_SOURCE_DIR STREQUAL CMAKE_BINARY_DIR)
    message(FATAL_ERROR "Do not build in-source. Please Remove CMakeCache.txt  and the CMakeFiles/ directory. Then build out of source!")
endif()


project(LaneDetector)

find_package(OpenCV REQUIRED)
find_package(OpenGL REQUIRED)
find_package(gflags REQUIRED)
find_package(glfw3 CONFIG REQUIRED)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include ${OpenCV_INCLUDE_DIRS} )

add_executable(test src/test.cpp)
target_link_libraries(test PRIVATE  gflags  ${OpenCV_LIBRARIES} ${OpenGL_LIBRARIES} glfw)
# target_compile_options(test PRIVATE "-framework OpenGL"  "-framework GLUT")

add_executable(lane_detetor src/lane_detector.cc)
target_link_libraries(lane_detetor PRIVATE  gflags  ${OpenCV_LIBRARIES} ${OpenGL_LIBRARIES} glfw)
