file(GLOB_RECURSE MPM_CPP_SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
)

file(GLOB_RECURSE MPM_HEADERS
    "${CMAKE_CURRENT_SOURCE_DIR}/*.h"
    "${CMAKE_CURRENT_SOURCE_DIR}/*.hpp"
)

set(MPM_ALL_SOURCES
    ${MPM_CPP_SOURCES}
    ${MPM_HEADERS}
)

add_executable(OpenGL-MPM ${MPM_ALL_SOURCES})

target_include_directories(OpenGL-MPM PRIVATE "${CMAKE_CURRENT_SOURCE_DIR}")

target_link_libraries(OpenGL-MPM PRIVATE
    glad
    glfw
    glm
    imgui
    assimp
)

target_compile_definitions(OpenGL-MPM PRIVATE
    MPM_SHADER_DIR="${CMAKE_SOURCE_DIR}/shaders"
    MPM_RESOURCES_DIR="${CMAKE_SOURCE_DIR}/resources")

source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}" PREFIX "Source Files" FILES ${MPM_CPP_SOURCES})
source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}" PREFIX "Header Files" FILES ${MPM_HEADERS})
