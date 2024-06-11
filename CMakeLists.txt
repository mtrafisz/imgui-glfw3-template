cmake_minimum_required (VERSION 3.5)

project (imgui_glfw_opengl3_template)
add_subdirectory (glfw) # build glfw as a static library

# set imgui backend to use glfw and opengl3
set (IMGUI_BACKENDS
     imgui/backends/imgui_impl_glfw.cpp
     imgui/backends/imgui_impl_opengl3.cpp)

# add our source files
file (GLOB SOURCES source/*.cpp)
add_executable (${PROJECT_NAME} ${SOURCES})

# include imgui and glfw headers
target_include_directories (${PROJECT_NAME} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/imgui
    ${CMAKE_CURRENT_SOURCE_DIR}/imgui/backends
    ${CMAKE_CURRENT_SOURCE_DIR}/glfw/include
)

# add imgui source files
file (GLOB IMGUI_SOURCES imgui/*.cpp)
target_sources (${PROJECT_NAME} PRIVATE ${IMGUI_SOURCES} ${IMGUI_BACKENDS})

# link glfw and opengl32
target_link_libraries (${PROJECT_NAME} PRIVATE glfw opengl32)
