cmake_minimum_required(VERSION 3.16 FATAL_ERROR)

set(PROJECT_NAME BattleCity)
project(${PROJECT_NAME})

add_executable(${PROJECT_NAME} 
    src/main.cpp
    src/Renderer/ShaderProgram.cpp
    src/Renderer/ShaderProgram.h
    src/Renderer/Texture2D.cpp
    src/Renderer/Texture2D.h
    src/Renderer/Sprite.cpp
    src/Renderer/Sprite.h
    src/Renderer/AnimatedSprite.cpp
    src/Renderer/AnimatedSprite.h
    src/Renderer/Renderer.cpp
    src/Renderer/Renderer.h



    src/Renderer/VertexArray.cpp
    src/Renderer/VertexArray.h
    src/Renderer/IndexBuffer.cpp
    src/Renderer/IndexBuffer.h

    src/Renderer/VertexBuffer.cpp
    src/Renderer/VertexBuffer.h
    src/Renderer/VertexBufferLayout.cpp
    src/Renderer/VertexBufferLayout.h


    src/Resources/ResourceManager.cpp
    src/Resources/ResourceManager.h
    src/Resources/stb_image.h
    src/Game/Game.cpp
    src/Game/Game.h
    src/Game/Tank.cpp
    src/Game/Tank.h
)

# C++17
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 17)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD_REQUIRED ON)

# GLFW options
option(GLFW_BUILD_DOCS "Build the GLFW documentation" OFF)
option(GLFW_BUILD_TESTS "Build the GLFW test programs" OFF)
option(GLFW_BUILD_EXAMPLES "Build the GLFW example programs" OFF)
option(GLFW_INSTALL "Generate installation target" OFF)

add_subdirectory(external/glfw)
target_link_libraries(${PROJECT_NAME} glfw)

add_subdirectory(external/glad)
target_link_libraries(${PROJECT_NAME} glad)

set_target_properties(${PROJECT_NAME} PROPERTIES 
    RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin/
)

include_directories(external/glm)
include_directories(external/rapidjson/include)
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    ${CMAKE_SOURCE_DIR}/res 
    $<TARGET_FILE_DIR:${PROJECT_NAME}>/res
)
