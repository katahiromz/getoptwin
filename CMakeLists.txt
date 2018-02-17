# CMakeLists.txt --- CMake project settings
#    ex) cmake -G "Visual Studio 9 2008" .
#    ex) cmake -DCMAKE_BUILD_TYPE=Release -G "MSYS Makefiles" .
##############################################################################

# CMake minimum version
cmake_minimum_required(VERSION 2.4)

# use new policy
cmake_policy(SET CMP0054 NEW)

# project name and language
project(getoptwin C)

##############################################################################

# check "getopt.h"
include(CheckIncludeFile)
check_include_file("getopt.h" HAVE_GETOPT_H)

if(HAVE_GETOPT_H)
    add_definitions(-DHAVE_GETOPT_H=1)

    add_executable(getopt_test getopt_test.c)

    if (NOT CMAKE_C_COMPILER_ID MATCHES "^(GNU|Clang)$")
        target_link_libraries(getopt_test getopt)
    endif()
else()
    add_executable(getopt_test getopt_test.c getoptwin.c)
endif()

##############################################################################
