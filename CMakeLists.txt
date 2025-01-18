cmake_minimum_required(VERSION 3.23)
project(wxMDArtProvider VERSION 1.0)

# Dependencies
find_package(wxWidgets REQUIRED COMPONENTS core base adv)
include(${wxWidgets_USE_FILE})

if(WIN32)
    include(Use_wxWindows)
endif()

# C++ Standard
# set(CMAKE_CXX_STANDARD_REQUIRED ON)
# set(CMAKE_CXX_EXTENSIONS OFF)
# if(NOT CMAKE_CXX_STANDARD OR CMAKE_CXX_STANDARD LESS 20)
# 	set(CMAKE_CXX_STANDARD 20)
# endif()

# Declare library
add_library(wxMDArtProvider)
target_include_directories(wxMDArtProvider INTERFACE include)

if(ADD_AWESOME_ART)
    file(GLOB AWSOURCES RELATIVE ${CMAKE_SOURCE_DIR} "src/wxAwesome*.cpp")
    target_sources(wxMDArtProvider PRIVATE ${AWSOURCES})
endif()

if(ADD_MDESIGN_ART)
    file(GLOB MDSOURCES RELATIVE ${CMAKE_SOURCE_DIR} "src/wxMaterial*.cpp")
    target_sources(
        wxMDArtProvider PRIVATE
        ${MDSOURCES}
    )
endif()

if(ADD_FLUENTUI_ART)
    file(GLOB FLSOURCES RELATIVE ${CMAKE_SOURCE_DIR} "src/wxFluentui*.cpp")
    target_sources(
        wxMDArtProvider PRIVATE
        ${FLSOURCES}
    )
endif()

if(ADD_SIMPLE_ART)
    target_sources(
        wxMDArtProvider PRIVATE
        src/wxSimpleIconsArt.cpp
    )
endif()

target_link_libraries(wxMDArtProvider ${wxWidgets_LIBRARIES})

# Add example to build
if(WITH_EXAMPLE)
    add_subdirectory(example)
endif()