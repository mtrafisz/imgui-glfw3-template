cmake_minimum_required (VERSION 3.5)

project (imgui_test)
add_subdirectory (glfw)

set (IMGUI_BACKENDS
    imgui/backends/imgui_impl_glfw.cpp
    imgui/backends/imgui_impl_opengl3.cpp
)

add_executable (${PROJECT_NAME} main.cpp)

target_include_directories (${PROJECT_NAME} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/imgui
    ${CMAKE_CURRENT_SOURCE_DIR}/imgui/backends
    ${CMAKE_CURRENT_SOURCE_DIR}/glfw/include
)

file (GLOB IMGUI_SOURCES imgui/*.cpp)
target_sources (${PROJECT_NAME} PRIVATE ${IMGUI_SOURCES} ${IMGUI_BACKENDS})

target_link_libraries (${PROJECT_NAME} PRIVATE glfw opengl32)