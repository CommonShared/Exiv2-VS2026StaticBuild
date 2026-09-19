cmake_minimum_required(VERSION 3.12...3.31)

project(
    libiconv
    LANGUAGES C
    VERSION 1.0.0)

add_library(libiconv STATIC
  "${CMAKE_CURRENT_SOURCE_DIR}/lib/compat.c"
  "${CMAKE_CURRENT_SOURCE_DIR}/lib/iconv.c"
  "${CMAKE_CURRENT_SOURCE_DIR}/libcharset/lib/localcharset.c")
target_include_directories(libiconv
  PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}"
  PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}/include"
  PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}/lib"
  PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}/libcharset/include")
add_library(libiconv_shared SHARED 
  "${CMAKE_CURRENT_SOURCE_DIR}/lib/compat.c"
  "${CMAKE_CURRENT_SOURCE_DIR}/lib/iconv.c"
  "${CMAKE_CURRENT_SOURCE_DIR}/libcharset/lib/localcharset.c")
target_include_directories(libiconv_shared
  PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}"
  PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}/include"
  PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}/lib"
  PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}/libcharset/include")

target_link_libraries(libiconv_shared PRIVATE "libiconv")
