cmake_minimum_required(VERSION 3.16)
project(mhypbase CXX)

#
# target: detours.lib
#
add_subdirectory(third_party/Detours-4.0.1)

#
# target: mhypbase.dll
#
add_library(mhypbase SHARED
  ${CMAKE_CURRENT_SOURCE_DIR}/src/dllmain.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/pch.cpp)
target_precompile_headers(mhypbase PRIVATE
  ${CMAKE_CURRENT_SOURCE_DIR}/include/pch.h)
target_compile_features(mhypbase PRIVATE cxx_std_20)
target_include_directories(mhypbase PRIVATE
  ${CMAKE_CURRENT_SOURCE_DIR}/include
  ${CMAKE_CURRENT_SOURCE_DIR}/third_party/simpleini-4.25)
target_link_libraries(mhypbase PRIVATE
  detours
  ntdll)
target_compile_definitions(mhypbase PRIVATE
  NOMINMAX)
