cmake_minimum_required(VERSION 3.25)

project(ImGuizmo LANGUAGES CXX)

if(PROJECT_IS_TOP_LEVEL)
    find_package(imgui CONFIG REQUIRED)
endif()

add_library(ImGuizmo)

target_sources(
  ImGuizmo
  PRIVATE src/ImGuizmo.cpp 
  PUBLIC FILE_SET
         HEADERS
         BASE_DIRS
         ./src
         FILES
         src/ImGuizmo.h
         )

add_library(ImGuizmo::ImGuizmo ALIAS ImGuizmo)

target_link_libraries(ImGuizmo PUBLIC imgui::imgui)

install(
  TARGETS ImGuizmo
  EXPORT ImGuizmo-targets
  FILE_SET HEADERS
  DESTINATION include/ImGuizmo/)

install(
  EXPORT ImGuizmo-targets
  DESTINATION lib/cmake/ImGuizmo
  NAMESPACE ImGuizmo::
  FILE ImGuizmo-targets.cmake)

install(FILES ${CMAKE_CURRENT_SOURCE_DIR}/ImGuizmoConfig.cmake
    DESTINATION lib/cmake/ImGuizmo)
