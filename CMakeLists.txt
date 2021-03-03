cmake_minimum_required(VERSION 3.9)
project(ChargeGuru)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake_modules/)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)

if(APPLE)
set(Qt5Core_DIR /usr/local/opt/qt/lib/cmake/Qt5Core)
set(Qt5Gui_DIR /usr/local/opt/qt/lib/cmake/Qt5Gui)
set(Qt5Widgets_DIR /usr/local/opt/qt/lib/cmake/Qt5Widgets)
set(Qt5Charts_DIR /usr/local/opt/qt/lib/cmake/Qt5Charts)
endif()

find_package(Qt5Core REQUIRED)
find_package(Qt5Gui REQUIRED)
find_package(Qt5Widgets REQUIRED)
find_package(Qt5Charts REQUIRED)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")

set(SOURCES
  main.cpp
  mainwindow.cpp
)

include_directories(${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_SOURCE_DIR}/../libb6)
link_directories(${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_SOURCE_DIR}/../libb6/lib/build)


add_executable(ChargeGuru ${SOURCES})
qt5_use_modules(ChargeGuru Core Gui Widgets Charts)

find_package(hidapi )
if (HIDAPI_FOUND)
    include_directories(${HIDAPI_INCLUDE_DIRS})
    target_link_libraries(ChargeGuru ${HIDAPI_LIBRARIES})
endif(HIDAPI_FOUND)

target_link_libraries(ChargeGuru b6)

