cmake_minimum_required(VERSION 3.16)
project(fluxions-renderer)

set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 17)

if (APPLE)
   include_directories(/usr/local/include)
   link_directories(/usr/local/lib)
endif()

include_directories(${PROJECT_SOURCE_DIR}/include)

add_library(${PROJECT_NAME}
   STATIC
	src/fluxions_renderer_config.cpp
	src/fluxions_renderer_context.cpp
	src/fluxions_renderer_framebuffer.cpp
	src/fluxions_renderer_gles30.cpp
	src/fluxions_renderer_gles30_snapshot.cpp
	src/fluxions_renderer_gpu_texture.cpp
	src/fluxions_renderer_object.cpp
	src/fluxions_renderer_program.cpp
	src/fluxions_renderer_sampler.cpp
	src/fluxions_renderer_shader.cpp
	src/fluxions_renderer_texture_2d.cpp
	src/fluxions_renderer_texture_cube.cpp
	src/fluxions_renderer_texture_object.cpp
	src/fluxions_renderer_uniform_blocks.cpp
	src/fluxions_renderer_utilities.cpp
	src/fluxions_shader_program_locations.cpp
   )

if(${CMAKE_VERSION} VERSION_GREATER "3.16.0")
    message("Fluxions Renderer using precompiled headers")
    target_precompile_headers(${PROJECT_NAME} PRIVATE src/fluxions_renderer_pch.cpp)
endif()

find_package(GLEW REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE GLEW::GLEW)
