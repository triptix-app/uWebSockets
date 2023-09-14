cmake_minimum_required(VERSION 3.19)
project(uWebSockets)

set(CMAKE_CXX_STANDARD 17)

file(
    GLOB SOURCES
    uSockets/src/*.c
    uSockets/src/eventing/*.c
)
add_library(uSockets ${SOURCES})
target_compile_definitions(uSockets PUBLIC WITH_IO_URING LIBUS_NO_SSL)
target_include_directories(uSockets PUBLIC uSockets/src)

add_library(uWebSockets INTERFACE)
target_include_directories(uWebSockets INTERFACE src)
target_link_libraries(uWebSockets INTERFACE uSockets zlibstatic)