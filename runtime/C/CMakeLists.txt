cmake_minimum_required(VERSION 2.6)
project(LIBANTLR3C C)

include_directories(include)

add_subdirectory(include)
add_subdirectory(src)

if(INSTALL_COMPONENT_IN_POSTBUILD)
	add_install_target(INSTALL_libantlr3c COMP_libantlr3c libantlr3c)
endif()
