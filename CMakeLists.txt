cmake_minimum_required(VERSION 3.2)
project(Reactive-Streams)

# Generate compilation database for use by YouCompleteMe.
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

# Common configuration for all build modes.
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wno-unused-parameter")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-omit-frame-pointer -momit-leaf-frame-pointer")

# Configuration for Debug build mode.
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -fsanitize=address")

include_directories(${CMAKE_SOURCE_DIR})

add_library(
  Reactive-Streams
  src/ReactiveStreams.h
  src/utilities/AllowanceSemaphore.h
  src/utilities/Ownership.h
  src/utilities/SmartPointers.h
  )

target_link_libraries(
  Reactive-Streams
  glog
  )

add_subdirectory(external/googletest EXCLUDE_FROM_ALL)
# EXCLUDE_FROM_ALL so 'make install' doesn't attempt installation of googletest

add_executable(
  tests
  src/examples/Examples.cpp
  src/test/AllowanceSemaphoreTest.cpp
  src/test/OwnershipTest.cpp
  src/test/SmartPointersTest.cpp
  )

target_link_libraries(
  tests
  gtest
  gmock
  gmock_main
  glog
  )

# EOF
