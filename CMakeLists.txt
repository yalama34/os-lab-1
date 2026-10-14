cmake_minimum_required(VERSION 3.16)

project(os_lab2 C)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    set(OS_SOURCE src/platform/os_linux.c)
else()
    message(FATAL_ERROR "Unsupported OS")
endif()

add_executable(parent
    src/parent.c
    src/line_utils.c
    ${OS_SOURCE}
)

add_executable(child
    src/child.c
    src/line_utils.c
)

set_target_properties(parent child PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}"
)

if(CMAKE_C_COMPILER_ID MATCHES "GNU|Clang")
    target_compile_options(parent PRIVATE -Wall -Wextra -Wpedantic)
    target_compile_options(child PRIVATE -Wall -Wextra -Wpedantic)
endif()