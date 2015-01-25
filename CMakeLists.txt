cmake_minimum_required(VERSION 2.8)
project(ygodeck-qt)

################################
# Compiler setup
################################

if (${CROSS_TARGET} STREQUAL "linux-64")
set(YGO_QT_VERSION "0.0.1")
set(CMAKE_AUTOMOC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(Qt5Widgets REQUIRED)

find_package(mindbw)
find_package(ygodata)
find_package(ygodeck)
find_package(zephyr)

include_directories(${MINDBW_INCLUDE_DIRS})
include_directories(${YGODATA_INCLUDE_DIRS})
include_directories(${YGODECK_INCLUDE_DIRS})
include_directories(${ZEPHYR_INCLUDE_DIRS})

################################
# Locate source
################################
file(GLOB_RECURSE SRC src/*.cpp)

################################
# Build targets
################################
add_executable(ygodeck-qt
    ${SRC})
target_link_libraries(ygodeck-qt
    ${YGODECK_LIBRARIES}
    ${ZEPHYR_LIBRARIES})

################################
# Export library
################################
export_project(
    NAME ygodeck-qt
    BINS ygodeck-qt
    VERSION ${YGO_QT_VERSION}
)

qt5_use_modules(ygodeck-qt Widgets)
endif()
