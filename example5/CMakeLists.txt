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



