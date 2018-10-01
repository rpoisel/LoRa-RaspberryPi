if (NOT EXISTS ${RADIOHEAD_SAMPLES_SRC})
  execute_process(COMMAND git clone --recursive https://github.com/idreamsi/RadioHead ${RADIOHEAD_SAMPLES_SRC})
endif ()

add_library(RadioHead STATIC
  ${RADIOHEAD_SAMPLES_SRC}/RHutil/RasPi.cpp
  ${RADIOHEAD_SAMPLES_SRC}/RH_RF95.cpp
  ${RADIOHEAD_SAMPLES_SRC}/RHDatagram.cpp
  ${RADIOHEAD_SAMPLES_SRC}/RHHardwareSPI.cpp
  ${RADIOHEAD_SAMPLES_SRC}/RHSPIDriver.cpp
  ${RADIOHEAD_SAMPLES_SRC}/RHGenericDriver.cpp
  ${RADIOHEAD_SAMPLES_SRC}/RHGenericSPI.cpp
)

target_include_directories(RadioHead PUBLIC
  ${RADIOHEAD_SAMPLES_SRC}
)

target_link_libraries(RadioHead PUBLIC
  bcm2835
)

target_compile_definitions(RadioHead PUBLIC
  RASPBERRY_PI
  BCM2835_NO_DELAY_COMPATIBILITY
  __BASEFILE__=__FILE__
)
