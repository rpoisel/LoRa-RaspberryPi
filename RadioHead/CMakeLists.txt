### RadioHead Samples
set(RADIOHEAD_SAMPLES_DIR ${CMAKE_BINARY_DIR}/RadioHead-Samples)
execute_process(COMMAND git clone --recursive https://github.com/idreamsi/RadioHead ${RADIOHEAD_SAMPLES_DIR})

### RadioHead Original
set(RADIOHEAD_ZIP ${CMAKE_BINARY_DIR}/RadioHead-1.86.zip)
set(RADIOHEAD_EXTRACT_DIR ${CMAKE_BINARY_DIR}/RadioHeadSrc)
set(RADIOHEADBASE ${RADIOHEAD_EXTRACT_DIR}/RadioHead)
file(DOWNLOAD http://www.airspayce.com/mikem/arduino/RadioHead/RadioHead-1.86.zip ${RADIOHEAD_ZIP} SHOW_PROGRESS)
file(MAKE_DIRECTORY ${RADIOHEAD_EXTRACT_DIR})
execute_process(
  COMMAND ${CMAKE_COMMAND} -E tar xzf ${RADIOHEAD_ZIP}
  WORKING_DIRECTORY ${RADIOHEAD_EXTRACT_DIR}
)
execute_process(
  COMMAND sed -i -e "s/RHutil\\/RasPi\\.h/RasPi.h/" ${RADIOHEADBASE}/RadioHead.h
)

add_library(RadioHead STATIC
  ${RADIOHEAD_SAMPLES_DIR}/RHutil/RasPi.cpp
  ${RADIOHEADBASE}/RH_RF95.cpp
)
  #${RADIOHEADBASE}/RHDatagram.cpp
  #${RADIOHEADBASE}/RHHardwareSPI.cpp
  #${RADIOHEADBASE}/RHSPIDriver.cpp
  #${RADIOHEADBASE}/RHGenericDriver.cpp
  #${RADIOHEADBASE}/RHGenericSPI.cpp

target_include_directories(RadioHead PUBLIC
  ${RADIOHEADBASE}
  ${RADIOHEAD_SAMPLES_DIR}/RHutil
)

target_link_libraries(RadioHead PUBLIC
  bcm2835
)

target_compile_definitions(RadioHead PUBLIC
  RASPBERRY_PI
  BCM2835_NO_DELAY_COMPATIBILITY
)
