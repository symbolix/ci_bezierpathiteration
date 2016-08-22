# ;--------------------------------------------------------------------------------
# ; Initials
# ;--------------------------------------------------------------------------------
cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(BezierPathIteration)

# ;--------------------------------------------------------------------------------
# ; Intro
# ;--------------------------------------------------------------------------------
MESSAGE(STATUS ";--------------------------------------------------------------------------------")
MESSAGE(STATUS "; <${PROJECT_NAME}> CMake Script v0.0.2.[8]")
MESSAGE(STATUS ";--------------------------------------------------------------------------------")

# ;--------------------------------------------------------------------------------
# ; libcinder Main Location
# ;--------------------------------------------------------------------------------
# Please make sure to have the environment variable $CINDER_PATH set to point to your
# libcinder location. The alternative flow below is a proprietary workflow that works
# only inside my environment.
if (DEFINED ENV{CINDER_PATH})
    # Environment constructs.
    set(CINDER_PATH $ENV{CINDER_PATH})
else(DEFINED ENV{CINDER_PATH})
    # Specific construct.
    set(current_package_slot "cinder-dev-0.9.1")
    
    # set(current_package_architecture "x86_64")
    set(current_package_architecture "")
    
    # Generic constructs.
    set(local_packages $ENV{UNIMOG_LOCAL_PACKAGES})
    set(current_package_absolute_path ${local_packages}/libs/${current_package_architecture}/${current_package_slot})
    
    # Make sure that the location is an absolute path.
    get_filename_component(CINDER_PATH "${current_package_absolute_path}" ABSOLUTE)
    
    # Verbose
    MESSAGE(STATUS "; <${PROJECT_NAME}> (DEBUG) Searching for package: ${current_package_slot}")
    MESSAGE(STATUS "; <${PROJECT_NAME}> (DEBUG) Fetching local packages from: ${local_packages}")
    MESSAGE(STATUS "; <${PROJECT_NAME}> (DEBUG) Current package architecture: ${current_package_architecture}")
    MESSAGE(STATUS "; <${PROJECT_NAME}> (DEBUG) Current package search path: ${current_package_absolute_path}")
endif()

# Verbose
MESSAGE(STATUS "; <${PROJECT_NAME}> (DEBUG) \${CINDER_PATH}\ returns: ${CINDER_PATH}")

if(IS_DIRECTORY ${CINDER_PATH})
    MESSAGE(STATUS "; <${PROJECT_NAME}> (DEBUG) \${CINDER_PATH}\ is a valid directory.")
else()
    MESSAGE(STATUS "; <${PROJECT_NAME}> (ERROR) \${CINDER_PATH}\ is a NOT valid path!")
    MESSAGE(FATAL_ERROR "Build process terminated.")
endif()

SET(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${PROJECT_SOURCE_DIR}/cmake)
MESSAGE(STATUS "; <${PROJECT_NAME}> (DEBUG) \${CMAKE_MODULE_PATH}\ returns: ${CMAKE_MODULE_PATH}")

# ;--------------------------------------------------------------------------------
# ; Project Specific Sources and Includes
# ;--------------------------------------------------------------------------------
set(PROJECT_SOURCE_FILES
    src/BezierPathIterationApp.cpp
)

set(PROJECT_INCLUDE_FILES
    src/BezierPathIterationApp.h
)

# ;--------------------------------------------------------------------------------
# ; Load Module
# ;--------------------------------------------------------------------------------
include(cinderMakeApp)

# ;--------------------------------------------------------------------------------
# ; Build the App
# ;--------------------------------------------------------------------------------
ci_make_app(
    SOURCES ${PROJECT_SOURCE_FILES}
    INCLUDES ${PROJECT_INCLUDE_FILES}
    CINDER_PATH ${CINDER_PATH}
    )

# vim: fdm=marker ts=4
