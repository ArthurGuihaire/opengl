cmake_minimum_required(VERSION 3.10)
project(MyProject)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# ----- directories ----------------------------------------------------------
set(SOURCE_DIR  "${CMAKE_SOURCE_DIR}/src")
set(INCLUDE_DIR "${CMAKE_SOURCE_DIR}/include")

# ----- sources --------------------------------------------------------------
file(GLOB SRC_FILES "${SOURCE_DIR}/*.cpp")
file(GLOB HEADER_FILES "${SOURCE_DIR}/*.c")

add_executable(MyApp
    ${SRC_FILES}
    ${HEADER_FILES}
)

# ----- headers --------------------------------------------------------------
target_include_directories(MyApp PRIVATE
    ${INCLUDE_DIR}        # glad.h  + KHR/
)

# ----- GLAD needs OpenGL ----------------------------------------------------
find_package(OpenGL REQUIRED)
target_link_libraries(MyApp PRIVATE OpenGL::GL)

# ----- GLFW -----------------------------------------------------------------
find_package(glfw3 3.3 REQUIRED)
target_link_libraries(MyApp PRIVATE glfw)

# ----- Copy shaders directory -----------------------------------------------
file(COPY ${CMAKE_SOURCE_DIR}/shaders DESTINATION ${CMAKE_BINARY_DIR})
