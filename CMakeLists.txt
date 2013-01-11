cmake_minimum_required(VERSION 2.8)
project(KoRE)

set(LIBRARY_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/lib)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/bin)

file(GLOB_RECURSE SOURCES src/*.cpp)
add_library(kore ${SOURCES})

set(IGNORE "-build/include")

#check code stlye
if(EXISTS "/usr/bin/python2")
    set(PYTHON_VER "python2")
else()
    set(PYTHON_VER "python")
endif()

add_custom_target(style
  COMMAND ${PYTHON_VER} scripts/cpplint.py --filter=${IGNORE} ${SOURCES}
)