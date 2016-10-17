# Created by Manuel Blum on 2011-05-25.
# Copyright 2013 University of Freiburg.

CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

PROJECT(libgp CXX C)

find_package(catkin REQUIRED COMPONENTS
  Eigen
  )

catkin_package(
  INCLUDE_DIRS include
  LIBRARIES RhAL
  CATKIN_DEPENDS Eigen
)

# if no option is given, standard is release
IF(NOT CMAKE_CONFIGURATION_TYPES AND NOT CMAKE_BUILD_TYPE)
   SET(CMAKE_BUILD_TYPE Release)
ENDIF(NOT CMAKE_CONFIGURATION_TYPES AND NOT CMAKE_BUILD_TYPE)

OPTION(BUILD_LIBGP_TESTS "Build tests" OFF)
OPTION(BUILD_LIBGP_EXAMPLES "Build examples" OFF)

SET(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_MODULE_PATH})

# ----- Add include directories -----
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR}/include)

# ----- Add sources -----
INCLUDE("Sources.cmake")

# ----- Add library target -----
ADD_LIBRARY(gp SHARED ${LIBGP_SRC} ${LIBGP_INTERFACES})

# ----- Add example targets -----
IF(BUILD_LIBGP_EXAMPLES)
  ADD_SUBDIRECTORY(examples)
ENDIF()

# ----- Testing -----
IF(BUILD_LIBGP_TESTS)
  ADD_SUBDIRECTORY(tests)
ENDIF()

