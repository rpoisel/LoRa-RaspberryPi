ExternalProject_Add(bcm2835_project
  URL http://www.airspayce.com/mikem/bcm2835/bcm2835-1.57.tar.gz
  CONFIGURE_COMMAND CC=${CMAKE_C_COMPILER} ./configure --host=armv6-logicals-linux-gnueabihf --prefix=<INSTALL_DIR>
  BUILD_IN_SOURCE TRUE
)

ExternalProject_Get_property(bcm2835_project INSTALL_DIR)

add_library(bcm2835 INTERFACE)

target_link_libraries(bcm2835 INTERFACE ${INSTALL_DIR}/lib/libbcm2835.a)

target_include_directories(bcm2835 INTERFACE ${INSTALL_DIR}/include)

add_dependencies(bcm2835 bcm2835_project)
