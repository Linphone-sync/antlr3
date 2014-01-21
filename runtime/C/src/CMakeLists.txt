cmake_minimum_required(VERSION 2.6)
project(ANTLR3C C)

set(SOURCE_FILES
    antlr3baserecognizer.c
    antlr3basetree.c
    antlr3basetreeadaptor.c
    antlr3bitset.c
    antlr3collections.c
    antlr3commontoken.c
    antlr3commontree.c
    antlr3commontreeadaptor.c
    antlr3commontreenodestream.c
    antlr3convertutf.c
    antlr3cyclicdfa.c
    antlr3debughandlers.c
    antlr3encodings.c
    antlr3exception.c
    antlr3filestream.c
    antlr3inputstream.c
    antlr3intstream.c
    antlr3lexer.c
    antlr3parser.c
    antlr3rewritestreams.c
    antlr3string.c
    antlr3tokenstream.c
    antlr3treeparser.c
)

if(WIN32)
set(LIBS ws2_32)
endif(WIN32)

add_library(antlr3c SHARED ${SOURCE_FILES})
set_target_properties(antlr3c PROPERTIES VERSION 3.4 SOVERSION 1)

target_link_libraries(antlr3c ${LIBS})

install(TARGETS antlr3c
	DESTINATION ${LIB_INSTALL_DIR}
	PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE
)
if(WIN32)
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/Debug/antlr3c.pdb
	DESTINATION ${LIB_INSTALL_DIR}
	PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE
)
endif()
endif(WIN32)
