cmake_minimum_required(VERSION 3.6)

project(OpenGLCube)

# Specify the path to the wxWidgets configuration executable if not automatically found
# Example for wxWidgets_CONFIG_EXECUTABLE is only necessary if CMake can't find wxWidgets automatically
set(wxWidgets_CONFIG_EXECUTABLE "${CMAKE_SOURCE_DIR}/../wxWidgets-3.2.4/build-gtk/wx-config")

find_package(wxWidgets REQUIRED COMPONENTS core base gl)
include(${wxWidgets_USE_FILE})

# Set OpenGL policy (prefer GLVND for modern systems)
cmake_policy(SET CMP0072 NEW)
set(OpenGL_GL_PREFERENCE GLVND)

# Find OpenGL and GLUT packages
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
 
# Include doiirectories for your project
include_directories(${OpenGL_INCLUDE_DIRS})
#include_directories(${CMAKE_SOURCE_DIR}/glad/include)
include_directories(${CMAKE_SOURCE_DIR}/include)

# Add source files
file(GLOB CPP_FILES ${CMAKE_SOURCE_DIR}/source/*.cpp)

# Define the executable
add_executable(executable ${CPP_FILES})

# Link libraries to your executable
target_link_libraries(executable ${wxWidgets_LIBRARIES} ${OPENGL_LIBRARIES} ${GLEW_LIBRARIES})