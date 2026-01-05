#
# Core
#

set(SOURCES
  vendor/stb/stb_image.h
  vendor/stb/stb_image.cpp
  src/Core/Application.h
  src/Core/Application.cpp
  src/Core/Window.h
  src/Core/Window.cpp
  src/Core/Layer.h
  src/Core/Layer.cpp
  src/Core/Event.h
  src/Core/WindowEvents.h
  src/Core/InputEvents.h
  src/Core/Renderer/Renderer.h
  src/Core/Renderer/Renderer.cpp
  src/Core/Renderer/Shader.h
  src/Core/Renderer/Shader.cpp
  src/Core/Renderer/GLUtils.h
  src/Core/Renderer/GLUtils.cpp
)

add_library(Core STATIC)

target_sources(Core PRIVATE ${SOURCES})

# Match VS filters to directory structure on disk
source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}" FILES ${SOURCES})

add_compile_definitions(
    GLFW_INCLUDE_NONE
)

target_link_libraries(Core glfw)
target_link_libraries(Core glad)
target_link_libraries(Core glm)


target_include_directories(Core PUBLIC "src" "vendor/stb")