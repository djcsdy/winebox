add_library(cpu callback.cpp cpu.cpp flags.cpp modrm.cpp core_full.cpp
    paging.cpp core_normal.cpp core_simple.cpp core_prefetch.cpp
    core_dyn_x86.cpp core_dynrec.cpp)