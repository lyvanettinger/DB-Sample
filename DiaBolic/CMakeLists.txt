﻿cmake_minimum_required (VERSION 3.8)

set( HEADER_FILES
	inc/camera.hpp
	inc/command_queue.hpp
	inc/dialogue_sample.hpp
	inc/dx12_helpers.hpp
	inc/d3dx12.h
	inc/glfw_app.hpp
	inc/renderer.hpp
	inc/resource_util.hpp
	inc/pipelines/geometry_pipeline.hpp
	inc/pipelines/ui_pipeline.hpp
)

set( SRC_FILES
	src/camera.cpp
	src/command_queue.cpp
	src/dialogue_sample.cpp
	src/dx12_helpers.cpp
	src/glfw_app.cpp
	src/main.cpp
	src/pch.h
	src/pch.cpp
	src/renderer.cpp
	src/resource_util.cpp
	src/pipelines/geometry_pipeline.cpp
	src/pipelines/ui_pipeline.cpp
)

add_executable( DiaBolic
    ${HEADER_FILES}
    ${SRC_FILES}
	src/pch.cpp
)

add_dependencies( DiaBolic copy-assets)

target_include_directories( DiaBolic
    PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/inc
)

target_link_libraries( DiaBolic
    PUBLIC DirectXTex
	PUBLIC glfw
	PRIVATE d3d12.lib
	PRIVATE dxgi.lib
	PRIVATE D3DCompiler.lib
	PRIVATE dxguid.lib
)

target_precompile_headers( DiaBolic
	PRIVATE "src/pch.h")

# Set Local Debugger Settings (Command Arguments and Environment Variables)
set( COMMAND_ARGUMENTS "-wd \"${CMAKE_SOURCE_DIR}\"" )