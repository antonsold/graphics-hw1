cmake_minimum_required(VERSION 3.0)
project(hw1)

set(CMAKE_CXX_STANDARD 14)

find_package(OpenGL REQUIRED)
add_subdirectory (external)
include_directories(
        external/AntTweakBar-1.16/include/
        external/glfw-3.1.2/include/
        external/glm-0.9.7.1/
        external/glew-1.13.0/include/
        external/assimp-3.0.1270/include/
        external/bullet-2.81-rev2613/src/
        .
)

set(ALL_LIBS
        ${OPENGL_LIBRARY}
        glfw
        GLEW_1130
        )

add_definitions(
        -DTW_STATIC
        -DTW_NO_LIB_PRAGMA
        -DTW_NO_DIRECT3D
        -DGLEW_STATIC
        -D_CRT_SECURE_NO_WARNINGS
)


add_executable(hw1 triangles/main.cpp common/shader.cpp
        common/shader.hpp)

target_link_libraries(hw1 ${ALL_LIBS})

add_custom_command(
        TARGET hw1 POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy "${CMAKE_CURRENT_BINARY_DIR}/${CMAKE_CFG_INTDIR}/hw1${CMAKE_EXECUTABLE_SUFFIX}" "${CMAKE_CURRENT_SOURCE_DIR}/triangles"
)

add_executable(hw1_figure figure/figure.cpp common/shader.cpp common/shader.hpp)
target_link_libraries(hw1_figure ${ALL_LIBS})
add_custom_command(
        TARGET hw1_figure POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy "${CMAKE_CURRENT_BINARY_DIR}/${CMAKE_CFG_INTDIR}/hw1_figure${CMAKE_EXECUTABLE_SUFFIX}" "${CMAKE_CURRENT_SOURCE_DIR}/figure"
)