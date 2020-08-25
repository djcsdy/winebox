cmake_minimum_required(VERSION 3.16)

set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake
        CACHE STRING "Vcpkg toolchain file")

include(cmake/VersionFromGit.cmake)
version_from_git(INCLUDE_HASH ON)

project(dosbox VERSION ${VERSION})

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

include(FindSDL)
if(NOT SDL_FOUND)
    message(FATAL_ERROR "Could not find SDL")
endif()

include(FindSDL_net)
if(NOT SDL_NET_FOUND)
    message(FATAL_ERROR "Could not find SDL_net")
endif()

include(FindPNG)
if(NOT PNG_FOUND)
    message(FATAL_ERROR "Could not find libpng.")
endif()

configure_file(include/config.h.in include/config.h)

add_definitions(${PNG_DEFINITIONS})

include_directories(${SDL_INCLUDE_DIR} ${SDL_NET_INCLUDE_DIRS}
        ${PNG_INCLUDE_DIRS} ${PROJECT_BINARY_DIR}/include include)

add_subdirectory(src)