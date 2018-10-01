set(BCM2835_ARCHIVE ${CMAKE_BINARY_DIR}/bcm2835-1.57.tar.gz)
set(BCM2835_DIR ${CMAKE_BINARY_DIR}/bcm2835-1.57)
if (NOT EXISTS ${BCM2835_ARCHIVE})
  file(DOWNLOAD http://www.airspayce.com/mikem/bcm2835/bcm2835-1.57.tar.gz ${BCM2835_ARCHIVE} SHOW_PROGRESS)
endif ()
execute_process(COMMAND cmake -E tar xf ${BCM2835_ARCHIVE} WORKING_DIRECTORY ${CMAKE_BINARY_DIR})
add_library(bcm2835 STATIC
  ${BCM2835_DIR}/src/bcm2835.c
)
target_include_directories(bcm2835 PUBLIC
  ${BCM2835_DIR}/src
)
