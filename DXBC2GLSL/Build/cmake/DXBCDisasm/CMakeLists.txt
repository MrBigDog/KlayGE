SET(EXE_NAME DXBCDisasm)

SET(HEADER_FILES
	${DXBC2GLSL_PROJECT_DIR}/Tools/DXBCDisasm/ASMGen.hpp
)
SET(SOURCE_FILES
	${DXBC2GLSL_PROJECT_DIR}/Tools/DXBCDisasm/ASMGen.cpp
	${DXBC2GLSL_PROJECT_DIR}/Tools/DXBCDisasm/DXBCDisasm.cpp
)

SOURCE_GROUP("Source Files" FILES ${SOURCE_FILES})
SOURCE_GROUP("Header Files" FILES ${HEADER_FILES})

LINK_DIRECTORIES(${DXBC2GLSL_PROJECT_DIR}/lib/${KLAYGE_PLATFORM_NAME})

ADD_EXECUTABLE(${EXE_NAME} ${SOURCE_FILES} ${HEADER_FILES})
ADD_DEPENDENCIES(${EXE_NAME} "DXBC2GLSLLib")

SET(EXTRA_LINKED_LIBRARIES
	debug DXBC2GLSLLib${KLAYGE_OUTPUT_SUFFIX}_d optimized DXBC2GLSLLib${KLAYGE_OUTPUT_SUFFIX}
	debug KFL${KLAYGE_OUTPUT_SUFFIX}_d optimized KFL${KLAYGE_OUTPUT_SUFFIX}
)

SET_TARGET_PROPERTIES(${EXE_NAME} PROPERTIES
	PROJECT_LABEL ${EXE_NAME}
	DEBUG_POSTFIX ${CMAKE_DEBUG_POSTFIX}
	OUTPUT_NAME ${EXE_NAME}
)

TARGET_LINK_LIBRARIES(${EXE_NAME}
	${EXTRA_LINKED_LIBRARIES})


ADD_POST_BUILD(${EXE_NAME} "")

INSTALL(TARGETS ${EXE_NAME}
	RUNTIME DESTINATION ${KLAYGE_BIN_DIR}
	LIBRARY DESTINATION ${KLAYGE_BIN_DIR}
	ARCHIVE DESTINATION ${KLAYGE_OUTPUT_DIR}
)

IF(MSVC)
	CREATE_VCPROJ_USERFILE(${EXE_NAME})
ENDIF()