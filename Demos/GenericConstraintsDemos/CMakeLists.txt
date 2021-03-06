set(SIMULATION_LINK_LIBRARIES AntTweakBar glew PositionBasedDynamics Simulation Utils)
set(SIMULATION_DEPENDENCIES AntTweakBar glew PositionBasedDynamics Simulation Utils)

if(WIN32)
  set(SIMULATION_LINK_LIBRARIES freeglut opengl32.lib glu32.lib ${SIMULATION_LINK_LIBRARIES})
  set(SIMULATION_DEPENDENCIES freeglut ${SIMULATION_DEPENDENCIES})
else()
  find_package(GLUT REQUIRED)
  find_package(OpenGL REQUIRED)

  set(SIMULATION_LINK_LIBRARIES
    ${SIMULATION_LINK_LIBRARIES}
    ${GLUT_LIBRARIES}
    ${OPENGL_LIBRARIES}
  )
endif()

add_executable(GenericParticleConstraintsDemo
	  GenericParticleConstraintsDemo.cpp
	  
	  GenericConstraintsModel.cpp
	  GenericConstraintsModel.h	  
	  GenericConstraints.cpp
	  GenericConstraints.h
	  
	  ${VIS_FILES}          
	  ${PROJECT_PATH}/Common/Common.h
	  
	  CMakeLists.txt
)

add_definitions(-DTW_NO_LIB_PRAGMA -DTW_STATIC)

find_package( Eigen3 REQUIRED )
include_directories( ${EIGEN3_INCLUDE_DIR} )
include_directories(${PROJECT_PATH}/extern/freeglut/include)
include_directories(${PROJECT_PATH}/extern/glew/include)

set_target_properties(GenericParticleConstraintsDemo PROPERTIES FOLDER "Demos")
set_target_properties(GenericParticleConstraintsDemo PROPERTIES DEBUG_POSTFIX ${CMAKE_DEBUG_POSTFIX})
set_target_properties(GenericParticleConstraintsDemo PROPERTIES RELWITHDEBINFO_POSTFIX ${CMAKE_RELWITHDEBINFO_POSTFIX})
set_target_properties(GenericParticleConstraintsDemo PROPERTIES MINSIZEREL_POSTFIX ${CMAKE_MINSIZEREL_POSTFIX})
add_dependencies(GenericParticleConstraintsDemo ${SIMULATION_DEPENDENCIES})
target_link_libraries(GenericParticleConstraintsDemo ${SIMULATION_LINK_LIBRARIES})
VIS_SOURCE_GROUPS()
