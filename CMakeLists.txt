cmake_minimum_required(VERSION 3.0)
project(tl-parser)

set(SOURCES crc32.h crc32.c tlc.c tl-parser.c tl-parser.h tl-parser-tree.h tl-tl.h portable_endian.h)

if (WIN32)
	list(APPEND SOURCES wingetopt.c wingetopt.h)
endif()
if (MSVC)
	set(CMAKE_EXE_LINKER_FLAGS "/SUBSYSTEM:CONSOLE")
endif()

add_executable(${PROJECT_NAME} ${SOURCES})
if (NOT WIN32)
	target_link_libraries(${PROJECT_NAME} m)
endif()
