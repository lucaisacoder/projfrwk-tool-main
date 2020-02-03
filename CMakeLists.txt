# CMake 最低版本号要求
cmake_minimum_required (VERSION 2.8)
project(dji_navigation)
include(${CMAKE_SOURCE_DIR}/../../tools/cmake/util/SetEnv.cmake)

include(${CMAKE_SOURCE_DIR}/../../tools/cmake/util/Print.cmake)

get_filename_component(SDK_SOURCE_DIR ${CMAKE_SOURCE_DIR}/../../ ABSOLUTE)

#include(${SDK_SOURCE_DIR}/tools/cmake/util/InstallConfig.cmake)

# Set SOURCES variable
set(DIR_SRCS .)
foreach(item ${DIR_SRCS})
    file(GLOB SOURCES_C ${item}/*.c)
    file(GLOB SOURCES_CPP ${item}/*.cpp)
    set(SOURCES ${SOURCES} ${SOURCES_C} ${SOURCES_CPP})
endforeach()

# Set HEADERS variable
set(DIR_INC_INN code/inc)
set(DIR_INC_PUB code/inc_pub)
set(DIR_INCS ${DIR_INC_INN} ${DIR_INC_PUB})
foreach(item ${DIR_INCS})
    file(GLOB HEADERS_H ${item}/*.h)
    file(GLOB HEADERS_HPP ${item}/*.hpp)
    set(HEADERS ${HEADERS} ${HEADERS_H} ${HEADERS_HPP})
endforeach()

#set(LIBRARY_TYPE SHARED)
#set(LIBRARY_TYPE STATIC)
#set(CMAKE_BUILD_TYPE DEBUG)
#set(CMAKE_BUILD_TYPE UNIT_TEST)
#set(HEADERS ${HEADERS_UT})
#set(SOURCES ${SOURCES_UT})
#set(DEFINITION -DUNIT_TEST)
set(REQ_LIBS core osal log)
set(REQ_LIBS_PATH ${SDK_SOURCE_DIR}/core/core/installed/lib/CMake/core ${SDK_SOURCE_DIR}/components/osal/installed/lib/CMake/osal ${SDK_SOURCE_DIR}/components/log/installed/lib/CMake/log)
#set(REQ_LIBS osal)
#set(REQ_LIBS_PATH ${SDK_SOURCE_DIR}/core/core)
#message("0000000 REQ_LIBS_PATH = ${REQ_LIBS_PATH}")
#include(${SDK_SOURCE_DIR}/tools/cmake/util/LibraryConfig.cmake)
include(${SDK_SOURCE_DIR}/tools/cmake/util/BinConfig.cmake) #只编译lib，最后link时候再对应生成bin
include(${SDK_SOURCE_DIR}/tools/cmake/util/Kconfig.cmake) 