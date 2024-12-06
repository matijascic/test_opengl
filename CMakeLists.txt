cmake_minimum_required(VERSION 3.27)
project(CAD2UT_Testbench)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(BUILD_DIR ${PROJECT_SOURCE_DIR}/build)
set(CMAKE_DEBUG_POSTFIX d)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG ${BUILD_DIR}/debug)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE ${BUILD_DIR}/release)

find_package( OpenGL REQUIRED )

include_directories(${OPENGL_INCLUDE_DIRS})
set(EXTERN_DIR ${PROJECT_SOURCE_DIR}/extern)
add_subdirectory(${EXTERN_DIR}/glfw)

include_directories(${GLFW_SOURCE_DIR}/deps)


set(CPP_FILES_DIR ${PROJECT_SOURCE_DIR}/src)
file(GLOB_RECURSE CPP_FILES ${CPP_FILES_DIR}/*.cpp ${CPP_FILES_DIR}/*.c)

set(HPP_FILES_DIR ${PROJECT_SOURCE_DIR}/include)
file(GLOB_RECURSE HPP_FILES ${CPP_FILES_DIR}/*.hpp ${CPP_FILES_DIR}/*.h)

include_directories(${HPP_FILES_DIR}/glad)

add_executable(cad2ut_testbench ${HPP_FILES} ${CPP_FILES} ${GLAD_GL} )

target_include_directories(cad2ut_testbench PRIVATE ${EXTERN_DIR}/glfw/include)
target_link_libraries(cad2ut_testbench ${OPENGL_LIBRARIES} glfw)