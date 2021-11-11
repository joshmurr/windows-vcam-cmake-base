cmake_minimum_required(VERSION 3.5)
project(vcam)

set(Baseclasses "${CMAKE_SOURCE_DIR}/dshowdeps/include")

set(DShow "${CMAKE_SOURCE_DIR}/dshowdeps/lib")

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")

add_subdirectory(src)
