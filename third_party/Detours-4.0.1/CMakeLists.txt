cmake_minimum_required(VERSION 3.16)
project(detours CXX)

#
# target: disolx64.obj
#
add_library(disolx64 OBJECT
  ${CMAKE_CURRENT_SOURCE_DIR}/src/disasm.cpp)
target_compile_definitions(disolx64 PRIVATE DETOURS_X64)

#
# target: detours.lib
#
add_library(detours STATIC
  ${CMAKE_CURRENT_SOURCE_DIR}/src/detours.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/modules.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/disasm.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/image.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/creatwth.cpp
  $<TARGET_OBJECTS:disolx64>)
target_include_directories(detours PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/src)
