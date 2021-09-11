cmake_minimum_required( VERSION 3.8 )

project( SimpleEngine )

find_package( OpenGL REQUIRED )

set(GLFW_ROOT_DIR "${PROJECT_SOURCE_DIR}/glfw")
set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE )
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE )
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE )

set(glew-cmake_BUILD_STATIC ON CACHE BOOL "" FORCE )
set(glew-cmake_BUILD_SHARED OFF CACHE BOOL "" FORCE )


option(SIMPLEENGINE_MAKE_DEMO "Put demo files in buildsystem too" OFF)

add_subdirectory( glfw )
add_subdirectory( glew )


set(ALL_INCLUDES
	"${PROJECT_SOURCE_DIR}/include"
	"${PROJECT_SOURCE_DIR}/glew/include"
	"${PROJECT_SOURCE_DIR}/glfw/include"
)

set(ALL_LIBS
	"glfw"
	"libglew_static"
)


set(SRCFILES
	src/playground.cpp
)

set(HEADERS

	include/spe/Game.hpp

	include/spe/graphics/opengl/ahh.h
	include/spe/graphics/opengl/Shader.hpp
)

#AUX_SOURCE_DIRECTORY(${CMAKE_CURRENT_SOURCE_DIR}/src SRCFILES)

add_library(SimpleEngine ${SRCFILES} ${HEADERS})

target_include_directories(SimpleEngine PRIVATE ${ALL_INCLUDES})
target_include_directories(SimpleEngine PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)
	
target_link_libraries(SimpleEngine ${ALL_LIBS})



if(MAKE_DEMO)

  #ballastic demo
  add_executable(demo_ballastic demo_ballastic/aaa.cpp)
  target_link_libraries(demo_ballastic ${ALL_LIBS})

endif()