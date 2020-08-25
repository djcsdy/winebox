include_directories(platform/visualc)

add_subdirectory(cpu)
add_subdirectory(debug)
add_subdirectory(dos)
add_subdirectory(fpu)
add_subdirectory(gui)
add_subdirectory(hardware)
add_subdirectory(ints)
add_subdirectory(libs)
add_subdirectory(misc)
add_subdirectory(shell)

add_executable(dosbox dosbox.cpp winres.rc)
target_link_libraries(dosbox cpu debug dos fpu gui hardware ints misc shell
        mame serial gui_tk ${SDL_LIBRARY} ${SDL_NET_LIBRARIES} ${PNG_LIBRARIES}
        OpenGL::GL)

if (WIN32)
    target_link_libraries(dosbox winmm ws2_32)
endif()