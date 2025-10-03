cmake_minimum_required(VERSION 3.15...3.27)
project(zombie-bindings)

set(ZOMBIE_BINDINGS_SRC_FILES
    "zombie_bindings.cpp"
    "zombie_bindings.h"
)

nanobind_add_module(zombie_bindings NOMINSIZE STABLE_ABI NB_STATIC ${ZOMBIE_BINDINGS_SRC_FILES})
target_link_libraries(zombie_bindings PRIVATE zombie)

install(TARGETS zombie_bindings LIBRARY DESTINATION zombie)

if(MSVC) 
    target_compile_options(zombie_bindings PRIVATE /bigobj) 
    file(GLOB_RECURSE TBB_DLLS CONFIGURE_DEPENDS "${CMAKE_BINARY_DIR}/**/tbb*.dll") 
    install(FILES ${TBB_DLLS} DESTINATION zombie) 

endif()