cmake_minimum_required(VERSION 3.19)
project(uWebSockets)

set(CMAKE_CXX_STANDARD 17)

file(
    GLOB SOURCES
    uSockets/src/*.c
    uSockets/src/eventing/*.c
#    uSockets/src/io_uring/*.c
#    uSockets/src/crypto/openssl.c
#    uSockets/src/crypto/sni_tree.cpp
)
add_library(uSockets ${SOURCES})
#target_link_libraries(uSockets ssl crypto)
target_compile_definitions(uSockets PUBLIC LIBUS_NO_SSL)
target_include_directories(uSockets PUBLIC uSockets/src)

add_library(uWebSockets INTERFACE)
target_include_directories(uWebSockets INTERFACE src)
target_link_libraries(uWebSockets INTERFACE uSockets zlibstatic)