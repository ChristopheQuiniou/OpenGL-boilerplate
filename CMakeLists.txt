cmake_minimum_required(VERSION 3.28)
project(Boilerplate-openGL)

# Set the path to GLFW library
set(GLFW_LIBRARY_PATH "${CMAKE_SOURCE_DIR}/src/vendors/GLFW/lib-arm64")

# Add GLFW library
find_library(GLFW_LIB_DYNAMIC glfw.3 HINTS ${GLFW_LIBRARY_PATH})
find_library(GLFW_LIB_STATIC glfw.a HINTS ${GLFW_LIBRARY_PATH})
if(NOT GLFW_LIB_DYNAMIC AND NOT GLFW_LIB_STATIC)
    message(FATAL_ERROR "GLFW library not found in ${GLFW_LIBRARY_PATH}")
endif()
# Add OpenGL library
find_package(OpenGL REQUIRED)

# Add your source files
set(SOURCES main.cpp)

# Add executable
add_executable(${PROJECT_NAME} ${SOURCES})

# Link GLFW library
if(GLFW_LIB_DYNAMIC)
    target_link_libraries(${PROJECT_NAME} ${GLFW_LIB_DYNAMIC})
else()
    target_link_libraries(${PROJECT_NAME} ${GLFW_LIB_STATIC})
endif()

# Link OpenGL library
target_link_libraries(${PROJECT_NAME} OpenGL::GL)