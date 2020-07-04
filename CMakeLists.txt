cmake_minimum_required(VERSION 3.12)
project(nfd)

set(CMAKE_CXX_STANDARD 17)

if(WIN32)
    file(GLOB SRC_FILES nfd_common.c nfd_win.cpp)
elseif(APPLE)
    file(GLOB SRC_FILES nfd_common.c nfd_cocoa.m)
elseif(UNIX)
    FIND_PACKAGE(PkgConfig REQUIRED)
    PKG_CHECK_MODULES(GTK3 REQUIRED gtk+-3.0)

    INCLUDE_DIRECTORIES(${GTK3_INCLUDE_DIRS})
    LINK_DIRECTORIES(${GTK3_LIBRARY_DIRS})

    ADD_DEFINITIONS(${GTK3_CFLAGS_OTHER})

    file(GLOB SRC_FILES nfd_common.c nfd_gtk.c)

endif()

add_library(nfd STATIC ${SRC_FILES})

if(UNIX)
    TARGET_LINK_LIBRARIES(nfd ${GTK3_LIBRARIES})
endif()
