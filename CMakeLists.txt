cmake_minimum_required(VERSION 3.27)
project(CAD2UT_Testbench)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS_DEBUG_INIT "-Wall")
set(CMAKE_CXX_FLAGS_RELEASE_INIT "-Wall")

set(BUILD_DIR ${PROJECT_SOURCE_DIR}/build)
set(CMAKE_DEBUG_POSTFIX d)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${BUILD_DIR}/Debug)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${BUILD_DIR}/Release)

find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS})

set(EXTERN_DIR ${PROJECT_SOURCE_DIR}/extern)
add_subdirectory(${EXTERN_DIR}/glfw)

include_directories(${GLFW_SOURCE_DIR}/deps)

set(SOURCE_FILES_DIR ${PROJECT_SOURCE_DIR}/src)
set(HEADER_DIR ${PROJECT_SOURCE_DIR}/include)
file(GLOB_RECURSE SRC_FILES ${SOURCE_FILES_DIR}/*.cpp ${SOURCE_FILES_DIR}/*.c ${HEADER_DIR}/*.hpp ${HEADER_DIR}/*.h)

set(IMGUI_DIR ${EXTERN_DIR}/imgui)
include_directories(${IMGUI_DIR})
include_directories(${IMGUI_DIR}/backends)
set(IMGUI_FILES 
    ${IMGUI_DIR}/imgui.h
    ${IMGUI_DIR}/imgui.cpp
    ${IMGUI_DIR}/imconfig.h
    ${IMGUI_DIR}/imgui_internal.h
    ${IMGUI_DIR}/imgui_draw.cpp
    ${IMGUI_DIR}/imgui_widgets.cpp
    ${IMGUI_DIR}/imgui_tables.cpp
    ${IMGUI_DIR}/backends/imgui_impl_glfw.h
    ${IMGUI_DIR}/backends/imgui_impl_glfw.cpp
    ${IMGUI_DIR}/backends/imgui_impl_opengl3.h
    ${IMGUI_DIR}/backends/imgui_impl_opengl3.cpp
    ${IMGUI_DIR}/backends/imgui_impl_opengl3_loader.h
    ) 

include_directories(${HEADER_DIR}/glad)
add_executable(cad2ut_testbench ${SRC_FILES} ${IMGUI_FILES} ${GLAD_GL})

target_include_directories(cad2ut_testbench PRIVATE ${EXTERN_DIR}/glfw/include)
target_link_libraries(cad2ut_testbench ${OPENGL_LIBRARIES} glfw)