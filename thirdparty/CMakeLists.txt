# ===========================================================================
# Third-party dependencies.
#
# Everything here is vendored (checked into thirdparty/). We intentionally do
# NOT use FetchContent so the build is fully offline and reproducible.
# ===========================================================================

# ---------------------------------------------------------------------------
# GLFW  (windowing + GL context + input)
# ---------------------------------------------------------------------------
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS    OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_DOCS     OFF CACHE BOOL "" FORCE)
set(GLFW_INSTALL        OFF CACHE BOOL "" FORCE)
add_subdirectory(glfw)
set_target_properties(glfw PROPERTIES FOLDER "thirdparty")

# ---------------------------------------------------------------------------
# GLM  (header-only math). Expose as an INTERFACE target.
# ---------------------------------------------------------------------------
add_library(glm INTERFACE)
target_include_directories(glm INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}/glm")
# Force GLM into radians + depth [0,1] conventions consistently everywhere.
target_compile_definitions(glm INTERFACE
    GLM_FORCE_RADIANS
    GLM_FORCE_DEPTH_ZERO_TO_ONE
    GLM_ENABLE_EXPERIMENTAL)

# ---------------------------------------------------------------------------
# GLAD  (OpenGL 4.6 Core loader, pre-generated into glad_generated/)
# ---------------------------------------------------------------------------
add_library(glad STATIC
    "${CMAKE_CURRENT_SOURCE_DIR}/glad_generated/src/gl.c")
target_include_directories(glad PUBLIC
    "${CMAKE_CURRENT_SOURCE_DIR}/glad_generated/include")
set_target_properties(glad PROPERTIES FOLDER "thirdparty")

# ---------------------------------------------------------------------------
# Assimp (FBX / model import)
# ---------------------------------------------------------------------------
set(ASSIMP_BUILD_ASSIMP_TOOLS OFF CACHE BOOL "" FORCE)
set(ASSIMP_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(ASSIMP_BUILD_SAMPLES OFF CACHE BOOL "" FORCE)
set(ASSIMP_INSTALL OFF CACHE BOOL "" FORCE)
set(ASSIMP_BUILD_ALL_IMPORTERS_BY_DEFAULT OFF CACHE BOOL "" FORCE)
set(ASSIMP_BUILD_FBX_IMPORTER ON CACHE BOOL "" FORCE)
set(ASSIMP_BUILD_OBJ_IMPORTER ON CACHE BOOL "" FORCE)
add_subdirectory(assimp)
set_target_properties(assimp PROPERTIES FOLDER "thirdparty")
set(IMGUI_DIR "${CMAKE_CURRENT_SOURCE_DIR}/imgui")
add_library(imgui STATIC
    "${IMGUI_DIR}/imgui.cpp"
    "${IMGUI_DIR}/imgui_draw.cpp"
    "${IMGUI_DIR}/imgui_tables.cpp"
    "${IMGUI_DIR}/imgui_widgets.cpp"
    "${IMGUI_DIR}/imgui_demo.cpp"
    "${IMGUI_DIR}/backends/imgui_impl_glfw.cpp"
    "${IMGUI_DIR}/backends/imgui_impl_opengl3.cpp")
target_include_directories(imgui PUBLIC
    "${IMGUI_DIR}"
    "${IMGUI_DIR}/backends")
# The OpenGL3 backend ships a self-contained loader (imgui_impl_opengl3_loader.h)
# that resolves its own GL function pointers. It coexists fine with our GLAD
# loader (both just call the platform GetProcAddress), so we do NOT override it.
target_link_libraries(imgui PUBLIC glfw)
set_target_properties(imgui PROPERTIES FOLDER "thirdparty")
