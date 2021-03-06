cmake_minimum_required(VERSION 2.8)
if(NOT (${CMAKE_MAJOR_VERSION}.${CMAKE_MINOR_VERSION} LESS 3.0))
	# only CMAKE 3.0 and greater supports this (NOT ... LESS because CMAKE does not have a GREATER_OR_EQUAL_TO conditional)
	# Not needed for older versions because older versions obviously use the old policy without specially requesting it
	cmake_policy(SET CMP0048 OLD)
	# ^^^ use the old VERSION variable behavior
endif()

# Name this project
set(LSTORE_PROJECT_NAME "ibp")
project(${LSTORE_PROJECT_NAME} C CXX)

# Include modules 
set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake)
include(CheckIncludeFile)

# Detect compiler flags.
# No-op for ibp

# Find additional dependencies.
find_package(ToolBox REQUIRED)
find_package(GOP REQUIRED)
include_directories(${TOOLBOX_INCLUDE_DIR} ${GOP_INCLUDE_DIR})
list(APPEND LIBS ${TOOLBOX_LIBRARY} ${GOP_LIBRARY})

# Additional Compiler flags.
# No-op for ibp

# common objects
set(LSTORE_PROJECT_OBJS
    ibp_config.c ibp_errno.c ibp_misc.c ibp_op.c ibp_sync.c ibp_types.c
    io_wrapper.c iovec_sync.c 
)

set(LSTORE_PROJECT_INCLUDES
    ibp_ClientLib.h ibp_errno.h ibp.h ibp_misc.h ibp_nfu.h ibp_op.h ibp_os.h
    ibp_protocol.h ibp_types.h iovec_sync.h io_wrapper.h
)

set(LSTORE_PROJECT_EXECUTABLES 
    ibp_perf ibp_test ibp_copyperf ibp_tool ibp_find_drive
)

# Common functionality is stored here
include(cmake/LStoreCommon.cmake)
