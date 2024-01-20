cmake_minimum_required(VERSION 3.27)
project(cloche_db)

set(CMAKE_CXX_STANDARD 17)

add_subdirectory(ext/src/boost EXCLUDE_FROM_ALL)

include_directories(${BOOST_LIBRARY_INCLUDES})

add_executable(cloche_db main.cpp)
