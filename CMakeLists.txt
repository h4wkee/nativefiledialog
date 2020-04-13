cmake_minimum_required(VERSION 3.12)
project(nfd)

set(CMAKE_CXX_STANDARD 17)

include_directories(src/include)

if(WIN32)
    file(GLOB SRC_FILES src/nfd_common.c src/nfd_win.cpp)
elseif(APPLE)
    file(GLOB SRC_FILES src/nfd_common.c src/nfd_cocoa.m)
endif()

add_library(nfd STATIC ${SRC_FILES})