#
# App
#

set(SOURCES
  src/Main.cpp
  src/AppLayer.h
  src/AppLayer.cpp
  src/VoidLayer.h
  src/VoidLayer.cpp
  src/OverlayLayer.h
  src/OverlayLayer.cpp
)

add_executable(App)

target_sources(App PRIVATE ${SOURCES})

# Match VS filters to directory structure on disk
source_group(TREE "${CMAKE_CURRENT_SOURCE_DIR}" FILES ${SOURCES})

add_compile_definitions(
  GLFW_INCLUDE_NONE
)

target_link_libraries(App
  PRIVATE
    Core
    -lstdc++exp
)


target_include_directories(App PRIVATE src)

set_target_properties(App PROPERTIES
  VS_DEBUGGER_WORKING_DIRECTORY "${CMAKE_SOURCE_DIR}/App"
)

add_custom_command(TARGET App POST_BUILD
  COMMAND ${CMAKE_COMMAND} -E copy_directory
          ${CMAKE_SOURCE_DIR}/App/Shaders
          $<TARGET_FILE_DIR:App>/Shaders
)

add_custom_command(TARGET App POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
            ${CMAKE_SOURCE_DIR}/App/Textures
            $<TARGET_FILE_DIR:App>/Textures
)