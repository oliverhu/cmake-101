include(CheckSymbolExists)

cmake_minimum_required(VERSION 3.1.0)
cmake_policy(SET CMP0048 NEW)

project (TestLibrary VERSION 1.0.0)

set(CMAKE_REQUIRED_LIBRARIES "m")
check_symbol_exists(log "math.h" HAVE_LOG) # Define macros
check_symbol_exists(exp "math.h" HAVE_EXP)

# First arg is the input file name, second is output file name.
configure_file(config.h.in config.h)

#For the shared library:
set ( PROJECT_LINK_LIBS libtestStudent.so )
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/bin)
link_directories( ${CMAKE_SOURCE_DIR}/studentlib_shared/build )

#For the static library:
#set ( PROJECT_LINK_LIBS libtestStudent.a )
#link_directories( ~/exploringBB/extras/cmake/studentlib_static/build )

include_directories(${CMAKE_SOURCE_DIR}/studentlib_shared/include)

add_executable(libtest libtest.cpp)
target_link_libraries(libtest ${PROJECT_LINK_LIBS} )
