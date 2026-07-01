cmake_minimum_required(VERSION 4.0)

project(ImGuizmo LANGUAGES CXX)

find_package(imgui CONFIG REQUIRED)

add_library(imguizmo STATIC)

target_sources(
  imguizmo
  PRIVATE src/ImGuizmo.cpp 
  PUBLIC FILE_SET
         HEADERS
         BASE_DIRS
         ./src
         FILES
         src/ImGuizmo.h
         )

add_library(imguizmo::imguizmo ALIAS imguizmo)

target_link_libraries(imguizmo PUBLIC imgui::imgui)

install(
  TARGETS imguizmo
  EXPORT imguizmo-targets
  FILE_SET HEADERS
  DESTINATION ${CMAKE_INSTALL_PREFIX}/include/imguizmo/)

install(
  EXPORT imguizmo-targets
  DESTINATION ${CMAKE_INSTALL_PREFIX}/lib/cmake/imguizmo
  NAMESPACE imguizmo::
  FILE imguizmo-targets.cmake)

install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/imguizmoConfig.cmake
    DESTINATION ${CMAKE_INSTALL_PREFIX}/lib/cmake/imguizmo)
