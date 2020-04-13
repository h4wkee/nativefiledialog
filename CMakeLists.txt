cmake_minimum_required(VERSION 3.12)
project(nfd)

set(CMAKE_CXX_STANDARD 17)

if(WIN32)
    file(GLOB SRC_FILES nfd_common.c nfd_win.cpp)
elseif(APPLE)
    file(GLOB SRC_FILES nfd_common.c nfd_cocoa.m)
endif()

add_library(nfd STATIC ${SRC_FILES})
