cmake_minimum_required(VERSION 3.2)

set(built_sources
	sphere-quad.h step_generic_stride1.cpp meep/meep-config.h
)
set(headers_files
	meep.hpp meep_internals.hpp meep/mympi.hpp meep/vec.hpp	
bicgstab.hpp meepgeom.hpp material_data.hpp adjust_verbosity.hpp
)

set(libmeep_sources
	array_slice.cpp anisotropic_averaging.cpp 		
bands.cpp boundaries.cpp bicgstab.cpp casimir.cpp 	
cw_fields.cpp dft.cpp dft_ldos.cpp energy_and_flux.cpp 
fields.cpp fields_dump.cpp fix_boundary_sources.cpp loop_in_chunks.cpp h5fields.cpp h5file.cpp 	
initialize.cpp integrate.cpp integrate2.cpp material_data.cpp monitor.cpp mympi.cpp 	
multilevel-atom.cpp near2far.cpp output_directory.cpp random.cpp 	
sources.cpp step.cpp step_db.cpp stress.cpp structure.cpp structure_dump.cpp		
susceptibility.cpp time.cpp update_eh.cpp mpb.cpp update_pols.cpp 	
vec.cpp step_generic.cpp meepgeom.cpp GDSIIgeom.cpp $(headers_files) $(built_sources)
)

add_library(libmeep $(libmeep_sources)) 

add_subdirectory(support)

target_link_libraries(libmeep PRIVATE meep_support_lib)


set(PRELUDE  "/* This file was automatically generated --- DO NOT EDIT */")

add_executable(sphere_quad sphere-quad.cpp)
add_custom_command(OUTPUT sphere-quad.h
	DEPENDS sphere_quad
	COMMAND echo $(PRELUDE) > sphere-quad.h
	COMMAND echo sphere_quad >> sphere-quad.h
	VERBATIM
)
add_custom_command(OUTPUT step_generic_stride1.cpp
	COMMAND echo $(PRELUDE) > step_generic_stride1.cpp
        COMMAND sed 's/LOOP_OVER/S1LOOP_OVER/g' $(top_srcdir)/src/step_generic.cpp | sed 's/step_curl/step_curl_stride1/' | sed 's/step_update_EDHB/step_update_EDHB_stride1/' | sed 's/step_beta/step_beta_stride1/') >> step_generic_stride1.cpp 
)


	
