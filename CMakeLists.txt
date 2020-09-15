cmake_minimum_required(VERSION 3.1)
enable_testing()

project(ColorUnmixing)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Release)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -pthread")
list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)

set(Qt5_DIR "/opt/qt511/")

find_package(Qt5 COMPONENTS Widgets DBus Gui REQUIRED)
message(STATUS "Qt5 library status:")
message(STATUS "    config: ${Qt5_DIR}")
message(STATUS "    version: ${Qt5_VERSION}")
message(STATUS "    libraries: ${Qt5_LIBS}")
message(STATUS "    include path: ${Qt5_INCLUDE_DIRS}")
add_executable(ColorUnmixingTest test.cpp)

add_subdirectory(unmixing)

target_link_libraries(ColorUnmixingTest ColorUnmixing Qt5::Widgets Qt5::DBus Qt5::Gui)



add_test(
  NAME test
  COMMAND $<TARGET_FILE:ColorUnmixingTest> ${CMAKE_SOURCE_DIR}/resources/leaves.jpg ${PROJECT_BINARY_DIR}
  WORKING_DIRECTORY ${PROJECT_BINARY_DIR}
)
