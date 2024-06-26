cmake_minimum_required(VERSION 3.24)
project(cpp)

set(CMAKE_CXX_STANDARD 23)

set(CMAKE_CXX_FLAGS_ASAN "-g -fsanitize=address,undefined -fno-sanitize-recover=all"
        CACHE STRING "Compiler flags in asan build"
        FORCE)

find_library(PARI_LIBRARY pari REQUIRED)
find_path(PARI_INCLUDE pari/pari.h REQUIRED)

find_package(Boost 1.84 REQUIRED)

add_executable(muranaghan-nakayama main.cpp lib.h ../../tools/partitions.h performance.h)
add_executable(test test.cpp lib.h ../../tools/partitions.h)

target_link_libraries(muranaghan-nakayama PRIVATE Boost::headers)
target_link_libraries(test PRIVATE Boost::headers)