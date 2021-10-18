cmake_minimum_required( VERSION 3.8 )

project( SimpleEngine )


option(SIMPLEENGINE_MAKE_DEMO "Put demo files in buildsystem too" OFF)

add_subdirectory( physics-engine )
add_subdirectory( graphic-engine )


set(ALL_INCLUDES
	"${PROJECT_SOURCE_DIR}/include"
	"${PROJECT_SOURCE_DIR}/physics-engine/include"
	"${PROJECT_SOURCE_DIR}/grapic-engine/include"
)

#Change library name as needed!
set(ALL_LIBS
	"spear"
	"sofre"
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