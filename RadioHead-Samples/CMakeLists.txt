add_executable(rf95_server
  ${RADIOHEAD_SAMPLES_SRC}/examples/raspi/rf95/rf95_server.cpp
)

target_link_libraries(rf95_server PUBLIC RadioHead)

add_executable(rf95_client
  ${RADIOHEAD_SAMPLES_SRC}/examples/raspi/rf95/rf95_client.cpp
)

target_link_libraries(rf95_client PUBLIC RadioHead)
