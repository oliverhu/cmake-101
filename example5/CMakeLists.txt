include(CMakePrintHelpers)
cmake_minimum_required(VERSION 3.1.0)
project (globalProject)

## Test function & output from cmake ##
message("EXP 1")
function(SIMPLE REQUIRED_ARG)
    message("Simple arguments: ${REQUIRED_ARG}, followed by ${ARGV}")
    set(${REQUIRED_ARG} "From SIMPLE" PARENT_SCOPE)
endfunction()

simple(This)
message("Output 1: ${This}")

message("EXP 2")
function(COMPLEX)
    cmake_parse_arguments(
        COMPLEX_PREFIX
        "SINGLE;ANOTHER"
        "ONE_VALUE;ALSO_ONE_VALUE"
        "MULTI_VALUES"
        ${ARGN}
    )
    message("COMPLEX_PREFIX_SINGLE: ${COMPLEX_PREFIX_SINGLE}")
    message("COMPLEX_PREFIX_ONE_VALUE: ${COMPLEX_PREFIX_ONE_VALUE}")
    message("COMPLEX_PREFIX_MULTI_VALUES: ${COMPLEX_PREFIX_MULTI_VALUES}")
endfunction()

complex(SINGLE ONE_VALUE value MULTI_VALUES some other values)

message("EXP 3: Run a Command at Config Time")
find_package(Git QUIET)

if(GIT_FOUND AND EXISTS "${PROJECT_SOURCE_DIR}/.git")
    execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
                    RESULT_VARIABLE GIT_SUBMOD_RESULT)
    if(NOT GIT_SUBMOD_RESULT EQUAL "0")
        message(FATAL_ERROR "git submodule update --init failed with ${GIT_SUBMOD_RESULT}, please checkout submodules")
    endif()
endif()

message("EXP 4: Run a Command at Build Time")
