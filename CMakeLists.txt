cmake_minimum_required(VERSION 3.11)

option(IMGUI_STATIC "build static library" ON)
option(IMGUI_SHARED "build shared library" OFF)
set(IMGUI_SOURCES
  "${CMAKE_CURRENT_SOURCE_DIR}/imgui.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/imgui_demo.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/imgui_draw.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/imgui_tables.cpp"
  "${CMAKE_CURRENT_SOURCE_DIR}/imgui_widgets.cpp"
)

if (DEFINED IMGUI_BACKENDS)
  list(APPEND IMGUI_SOURCES ${IMGUI_BACKENDS})
endif()

if (IMGUI_STATIC)
  add_library(imgui STATIC ${IMGUI_SOURCES})
elseif (IMGUI_SHARED)
  add_library(imgui SHARED ${IMGUI_SOURCES})
endif()

target_compile_definitions(imgui PUBLIC
  IMGUI_USE_WCHAR32
  IMGUI_DEFINE_MATH_OPERATORS
)
target_include_directories(
  imgui PRIVATE
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_SOURCE_DIR}/backends
)

