add_library(pico_analog_microphone INTERFACE)

target_sources(pico_analog_microphone INTERFACE
    ${CMAKE_CURRENT_LIST_DIR}/analog_microphone.c
)

target_include_directories(pico_analog_microphone INTERFACE
    ${CMAKE_CURRENT_LIST_DIR}/include
)


target_link_libraries(pico_analog_microphone INTERFACE hardware_adc hardware_dma)