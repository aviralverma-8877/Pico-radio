cmake_minimum_required(VERSION 3.13)

include(pico_sdk_import.cmake)

project(fm_project C CXX ASM)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

pico_sdk_init()

add_subdirectory(fm_rda5807)
add_subdirectory(rds_parser)
add_subdirectory(pico-ss-oled build)
add_subdirectory(pico_analog_microphone)

add_executable(fm_example fm_example.cpp usb_descriptors.c usb_microphone.c)

pico_enable_stdio_usb(fm_example 1)
pico_enable_stdio_uart(fm_example 0)

pico_add_extra_outputs(fm_example)

target_compile_options(fm_example PRIVATE -Wall -Wextra)
target_include_directories(fm_example PRIVATE ${CMAKE_CURRENT_LIST_DIR})

target_link_libraries(fm_example  
    tinyusb_device
    pico_analog_microphone
    hardware_pwm
    fm_rda5807
    rds_parser
    pico_stdlib
    pico_ss_oled
    pico_multicore
    )
