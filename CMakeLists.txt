cmake_minimum_required(VERSION 3.0)
project(tl-parser)

set(SOURCES crc32.h crc32.c tlc.c tl-parser.c tl-parser.h tl-parser-tree.h tl-tl.h portable_endian.h)

if (WIN32)
	add_definitions("-D_CRT_SECURE_NO_WARNINGS")
	list(APPEND SOURCES wgetopt.c wgetopt.h)
	if (MSVC)
		set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} /SUBSYSTEM:CONSOLE")
		set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} /utf-8")
	endif()
endif()

# Set the output directories to the cmake build directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG .)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELEASE .)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_RELWITHDEBINFO .)

add_executable(${PROJECT_NAME} ${SOURCES})
if (NOT WIN32)
	target_link_libraries(${PROJECT_NAME} m)
endif()
