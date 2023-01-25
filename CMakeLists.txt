cmake_minimum_required(VERSION 3.2)a
project(Meep 1.0)


set(SHARED_VERSION_INFO "30:0:0")




add_subdirectory(src)
add_subdirectory(tests)

configure_file(${CMAKE_CURRENT_LIST_DIR}/src/meep/meep-config.h.in ${CMAKE_CURRENT_LIST_DIR}/src/meep/meep-config.h)
