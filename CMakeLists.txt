cmake_minimum_required(VERSION 3.16)
project(dosbox)

include(CheckIncludeFileCXX)

CHECK_INCLUDE_FILE_CXX(unistd.h HAS_UNISTD_H)
CHECK_INCLUDE_FILE_CXX(io.h HAS_IO_H)

if(HAS_UNISTD_H)
    add_compile_definitions("UNISTD_H=<unistd.h>")
elseif(HAS_IO_H)
    add_compile_definitions("UNISTD_H=<io.h>")
else()
    message(FATAL_ERROR "Could not find unistd.h or io.h.")
endif()

add_executable(dosbox src/dosbox.cpp)