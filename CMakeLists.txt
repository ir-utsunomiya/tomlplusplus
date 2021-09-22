cmake_minimum_required(VERSION 3.14)

project(
    tomlplusplus
    VERSION 2.5.0
    DESCRIPTION "Header-only TOML config file parser and serializer for C++17 (and later!)"
    HOMEPAGE_URL "https://marzer.github.io/tomlplusplus/"
    LANGUAGES CXX
)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -DBOOST_NO_AUTO_PTR")
set_directory_properties(PROPERTIES COMPILE_OPTIONS "-std=c++17")

add_library(tomlplusplus_tomlplusplus INTERFACE)
add_library(tomlplusplus::tomlplusplus ALIAS tomlplusplus_tomlplusplus)

set_property(
    TARGET tomlplusplus_tomlplusplus PROPERTY
    EXPORT_NAME tomlplusplus
)

target_include_directories(
  tomlplusplus_tomlplusplus
  INTERFACE
  "$<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>"
)

include(GNUInstallDirs)

install(TARGETS tomlplusplus_tomlplusplus
  EXPORT tomlplusplus-export
  LIBRARY       DESTINATION lib
  ARCHIVE       DESTINATION lib
  INCLUDES      DESTINATION include
  PUBLIC_HEADER DESTINATION include
)

install(
  DIRECTORY "${PROJECT_SOURCE_DIR}/include/"
  DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
  COMPONENT tomlplusplus_Development
)

install( EXPORT tomlplusplus-export
  FILE tomlplusplus-config.cmake
  DESTINATION share/cmake/tomlplusplus/
  EXPORT_LINK_INTERFACE_LIBRARIES
)

