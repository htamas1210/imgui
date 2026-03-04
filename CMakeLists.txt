cmake_minimum_required(VERSION 3.15)
project(ImGui LANGUAGES CXX)

# 1. Create the Static Library and list all source files
add_library(ImGui STATIC
    imconfig.h
    imgui.h
    imgui.cpp
    imgui_draw.cpp
    imgui_internal.h
    imgui_tables.cpp
    imgui_widgets.cpp
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h
    imgui_demo.cpp
    misc/cpp/imgui_stdlib.cpp
    misc/cpp/imgui_stdlib.h
    backends/imgui_impl_sdl3.cpp
    backends/imgui_impl_sdl3.h
    backends/imgui_impl_sdlrenderer3.cpp
    backends/imgui_impl_sdlrenderer3.h
)

# 2. Enforce C++17 (from your cppdialect "C++17" filter)
target_compile_features(ImGui PUBLIC cxx_std_17)

# Disable static runtime (Equivalent to staticruntime "off")
set_property(TARGET ImGui PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>DLL")

# 3. Include directories
# Using PUBLIC here means any project that links ImGui will automatically get this include directory too!
target_include_directories(ImGui PUBLIC
    "${CMAKE_CURRENT_SOURCE_DIR}"
)

target_include_directories(ImGui PRIVATE "../sdl3/include")

# 4. OS Specific Filters
if(UNIX AND NOT APPLE)
    # Equivalent to pic "On" in Linux
    set_property(TARGET ImGui PROPERTY POSITION_INDEPENDENT_CODE ON)
endif()
