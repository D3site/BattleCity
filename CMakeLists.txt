cmake_minimum_required(VERSION 4.0.1 FATAL_ERROR)
set(PROJECT_NAME BattleCity)
project(${PROJECT_NAME})

add_executable(${PROJECT_NAME} src/main.cpp)

option(GLFW_BUILD_DOCS "Build the GLFW documentation" OFF)
option(GLFW_BUILD_TESTS "Build the GLFW test programs" ${GLFW_STANDALONE} OFF)
option(GLFW_BUILD_EXAMPLES "Build the GLFW example programs" ${GLFW_STANDALONE} OFF)
option(GLFW_INSTALL "Generate installation target" OFF)

add_subdirectory(external/glfw)
target_link_libraries(${PROJECT_NAME} glfw)