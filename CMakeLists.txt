#---------------------------------------------------#
#          CMake Project Configuration              #
#---------------------------------------------------#
# CMake will issue a warning if you don't set this
cmake_minimum_required( VERSION 2.8 )

# If you don't name the project, it will take the default name "Project"
# Note: this must be set in the beginning of the CMakeLists file
project( sample_texture_projection )

# Add the extra cmake module script path
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake ${CMAKE_MODULE_PATH})

#---------------------------------------------------#
#              OpenGL Configuration                 #
#---------------------------------------------------#
# Automatically find GL libraries
find_package( OpenGL )
find_package( GLUT REQUIRED )

#---------------------------------------------------#
#              Project Files                        #
#---------------------------------------------------#
# List source files in a variable so we can use it later more conveniently
set( LAB_SRCS
	projtex.c
	texture.c
)

set( LAB_HEADERS
	texture.h
)

#---------------------------------------------------#
#               Project Configuration               #
#---------------------------------------------------#
# Add all sources defined above to the program
include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/include ${GLUT_INCLUDE_DIR} ${OPENGL_INCLUDE_DIR} )

link_directories( ${CMAKE_BINARY_DIR}/bin ${GLUT_LIBRARY_PATH} )

# Add _d to the library in debug
set( CMAKE_DEBUG_POSTFIX _d )

add_executable( sample_texture_projection ${LAB_HEADERS} ${LAB_SRCS} )

target_link_libraries( sample_texture_projection ${GLUT_LIBRARIES} ${OPENGL_LIBRARIES} )

# include math libraries
IF(UNIX)
  target_link_libraries(sample_texture_projection m)
ENDIF(UNIX)
