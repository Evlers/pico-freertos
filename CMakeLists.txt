cmake_minimum_required(VERSION 3.13)

# Pull in SDK (must be before project)
include(pico_sdk_import.cmake)

# Pull in FreeRTOS
set(FREERTOS_KERNEL_PATH ${CMAKE_CURRENT_LIST_DIR}/freertos)
include(FreeRTOS_Kernel_import.cmake)

# Project name
project(pico-freertos)

pico_sdk_init()

# Configuration projects
add_executable(pico-freertos
    src/main.c
)

target_include_directories(pico-freertos PRIVATE
    include/
)

target_link_libraries(pico-freertos PRIVATE
    pico_stdlib
    FreeRTOS-Kernel
    FreeRTOS-Kernel-Heap4
)

target_compile_options(pico-freertos PRIVATE -Wall)

# Run the entire project in SRAM
# pico_set_binary_type(pico-freertos copy_to_ram)

pico_add_extra_outputs(pico-freertos)
