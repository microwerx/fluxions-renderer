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
    )

if(${CMAKE_VERSION} VERSION_GREATER "3.16.0")
    message("Fluxions SSG using precompiled headers")
    target_precompile_headers(${PROJECT_NAME} PRIVATE src/fluxions_ssg_pch.cpp)
endif()

find_package(GLEW REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE GLEW::GLEW)
