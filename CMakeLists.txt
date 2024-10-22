cmake_minimum_required(VERSION 3.10)
project("CubismFramework")

set(LIB_NAME Framework)
set(FRAMEWORK_SOURCE "OpenGL")

# Force static library.
add_library(${LIB_NAME} SHARED)

find_package(CubismCore REQUIRED)
find_package(Qt6 REQUIRED COMPONENTS OpenGLWidgets)

add_subdirectory(src)

# Add include path.
target_include_directories(${LIB_NAME}
  PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/src
  PRIVATE
    ${RENDER_INCLUDE_PATH}
)

# Deprecated functions
# The following expressions are written for compatibility
# and will be removed in a future release.

# Add core include.
target_include_directories(${LIB_NAME}
  PRIVATE
  ${CubismCore_INCLUDE_DIRS}
  Qt6::OpenGLWidgets
)

# Link the required libraries.
target_link_libraries(${LIB_NAME}
  PRIVATE
    Qt6::OpenGLWidgets
    ${CubismCore_LIBRARIES}      # Link CubismCore libraries
)
