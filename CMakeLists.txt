cmake_minimum_required(VERSION 3.12)
project(LoRa)

set(RADIOHEAD_SAMPLES_SRC ${CMAKE_BINARY_DIR}/RadioHead-Samples-Git)

add_subdirectory(bcm2835)
add_subdirectory(RadioHead)
add_subdirectory(RadioHead-Samples)
