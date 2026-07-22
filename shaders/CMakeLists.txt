file(GLOB_RECURSE SHADER_FILES
    "${CMAKE_SOURCE_DIR}/shaders/*.vert"
    "${CMAKE_SOURCE_DIR}/shaders/*.frag"
    "${CMAKE_SOURCE_DIR}/shaders/*.geom"
    "${CMAKE_SOURCE_DIR}/shaders/*.tesc"
    "${CMAKE_SOURCE_DIR}/shaders/*.tese"
    "${CMAKE_SOURCE_DIR}/shaders/*.comp"
    "${CMAKE_SOURCE_DIR}/shaders/*.glsl"
    "${CMAKE_SOURCE_DIR}/shaders/*.hlsl"
    "${CMAKE_SOURCE_DIR}/shaders/*.spv"
)
add_custom_target(ShaderFiles SOURCES ${SHADER_FILES})
set_target_properties(ShaderFiles PROPERTIES
    FOLDER "Shaders"
)