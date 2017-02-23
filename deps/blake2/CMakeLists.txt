cmake_minimum_required(VERSION 3.2)

project(blake2)

set(BLAKE2_INCLUDE_DIR
	"${CMAKE_CURRENT_SOURCE_DIR}/src" 
		CACHE PATH "blake2 include path")

include_directories(
	${LIBblake2_INCLUDE_DIRS}
	src
)

if(WIN32)
	if(MSVC)
		add_compile_options("$<$<CONFIG:RelWithDebInfo>:/MT>")
	endif()
	add_definitions(
		-Dinline=_inline
		-Drestrict=__restrict)
endif()

set(blake2_SOURCES
	src/blake2b-ref.c)

if (WIN32)
	SET_SOURCE_FILES_PROPERTIES(
		${blake2_SOURCES}
			PROPERTIES LANGUAGE C)
endif()

add_library(blake2 STATIC
	${blake2_SOURCES})