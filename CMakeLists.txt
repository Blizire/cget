cmake_minimum_required(VERSION 3.16.0)

# point to header files
include_directories(libs/curl/include)

# set project name
project(cget)

# compile as executable
add_executable (cget src/cget.c)

# add imported library
add_library(libcurl STATIC IMPORTED)

# point imported target to actual files
set_property(TARGET libcurl PROPERTY 
				IMPORTED_LOCATION ${PROJECT_SOURCE_DIR}/libs/curl/lib/libcurl.dll.a)

target_link_libraries(cget libcurl)

# set location of binary
add_custom_command(TARGET cget
                   POST_BUILD
                   COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_FILE:cget> ${PROJECT_SOURCE_DIR}/bin)