############################################################################
# CMakeLists.txt
# Copyright (C) 2014  Belledonne Communications, Grenoble France
#
############################################################################
#
# This program is free software; you can redistribute it and/or
# modify it under the terms of the GNU General Public License
# as published by the Free Software Foundation; either version 2
# of the License, or (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place - Suite 330, Boston, MA  02111-1307, USA.
#
############################################################################

if(WIN32)
	set(SHARED_LIB_INSTALL_DIR bin)
else(WIN32)
	set(SHARED_LIB_INSTALL_DIR lib)
endif(WIN32)
set(STATIC_LIB_INSTALL_DIR lib)

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
	${CMAKE_CURRENT_BINARY_DIR}/antlr3config.h
)
set_source_files_properties(${CMAKE_CURRENT_BINARY_DIR}/antlr3config.h PROPERTIES GENERATED ON)

if(WIN32)
	set(LIBS ws2_32)
endif(WIN32)

if(${ENABLE_STATIC})
	add_library(antlr3c-static STATIC ${SOURCE_FILES})
	set_target_properties(antlr3c-static PROPERTIES OUTPUT_NAME antlr3c)
	target_link_libraries(antlr3c-static ${LIBS})
	install(TARGETS antlr3c-static
		DESTINATION ${STATIC_LIB_INSTALL_DIR}
		PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE
	)
else(${ENABLE_STATIC})
	add_library(antlr3c SHARED ${SOURCE_FILES})
	set_target_properties(antlr3c PROPERTIES VERSION 3.4 SOVERSION 1)
	target_link_libraries(antlr3c ${LIBS})
	install(TARGETS antlr3c
		DESTINATION ${SHARED_LIB_INSTALL_DIR}
		PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE
	)
	if(MSVC)
		if(CMAKE_BUILD_TYPE STREQUAL "Debug")
			install(FILES ${CMAKE_CURRENT_BINARY_DIR}/Debug/antlr3c.pdb
				DESTINATION ${SHARED_LIB_INSTALL_DIR}
				PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE
			)
		endif(CMAKE_BUILD_TYPE STREQUAL "Debug")
	endif(MSVC)
endif(${ENABLE_STATIC})
