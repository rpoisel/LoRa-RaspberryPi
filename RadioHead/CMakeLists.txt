set(RADIOHEAD_SAMPLES_DIR ${CMAKE_BINARY_DIR}/RadioHead-Samples)
execute_process(COMMAND git clone --recursive https://github.com/idreamsi/RadioHead ${RADIOHEAD_SAMPLES_DIR})

add_library(RadioHead STATIC
  ${RADIOHEAD_SAMPLES_DIR}/RHutil/RasPi.cpp
  ${RADIOHEAD_SAMPLES_DIR}/RH_RF95.cpp
  ${RADIOHEAD_SAMPLES_DIR}/RHDatagram.cpp
  ${RADIOHEAD_SAMPLES_DIR}/RHHardwareSPI.cpp
  ${RADIOHEAD_SAMPLES_DIR}/RHSPIDriver.cpp
  ${RADIOHEAD_SAMPLES_DIR}/RHGenericDriver.cpp
  ${RADIOHEAD_SAMPLES_DIR}/RHGenericSPI.cpp
)

target_include_directories(RadioHead PUBLIC
  ${RADIOHEAD_SAMPLES_DIR}
)

target_link_libraries(RadioHead PUBLIC
  bcm2835
)

target_compile_definitions(RadioHead PUBLIC
  RASPBERRY_PI
  BCM2835_NO_DELAY_COMPATIBILITY
  __BASEFILE__=__FILE__
)
