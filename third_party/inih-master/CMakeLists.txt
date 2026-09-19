cmake_minimum_required(VERSION 3.12...3.31)

project(
    inih_inireader
    LANGUAGES C CXX
    VERSION 1.0.0)

add_library(inih_inireader STATIC "${CMAKE_CURRENT_SOURCE_DIR}/cpp/INIReader.cpp")
add_library(inih STATIC "${CMAKE_CURRENT_SOURCE_DIR}/ini.c")

add_library(inih_inireader_shared SHARED "${CMAKE_CURRENT_SOURCE_DIR}/cpp/INIReader.cpp" "${CMAKE_CURRENT_SOURCE_DIR}/ini.c")
add_library(inih_shared SHARED "${CMAKE_CURRENT_SOURCE_DIR}/ini.c")

target_link_libraries(inih_inireader_shared PRIVATE "inih_inireader" PRIVATE "inih")
