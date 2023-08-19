cmake_minimum_required(VERSION 3.2)
project(Meep 1.0)


set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

execute_process(COMMAND ./version.sh 1.27.0-beta
RESULT_VARIABLE MEEP_VERSION
WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
)

set(SHARED_VERSION_INFO "31:0:0")


add_subdirectory(src)
add_subdirectory(tests)

configure_file(${CMAKE_CURRENT_LIST_DIR}/src/meep/meep-config.h.in ${CMAKE_CURRENT_LIST_DIR}/src/meep/meep-config.h)




option(MEEP_SINGLE "Compile in single precision" OFF)

option(MEEP_SWIG_PYTHON_THREADS "enable swig threads for python bindings" OFF)
option(MEEP_SWIG_PYTHON_DEBUG "enable swig debug for python bindings"
	OFF)

option(MEEP_MPI "enable mpi parallelisation" OFF)


find_package(MPI REQUIRED)
message(STATUS "Run: ${MPIEXEC} ${MPIEXEC_NUMPROC_FLAG} ${MPIEXEC_MAX_NUMPROCS} ${MPIEXEC_PREFLAGS} EXECUTABLE ${MPIEXEC_POSTFLAGS} ARGS")





configure_file(${CMAKE_CURRENT_LIST_DIR}/meep-pkconfig.in ${CMAKE_CURRENT_LIST_DIR}/meep-pkgconfig)
