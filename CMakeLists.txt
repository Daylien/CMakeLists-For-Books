cmake_minimum_required(VERSION 3.6)


# Global variables to set


set(project_name "My Book")         # Set the project name
set(lang "c")                       # Set the compile language c or cpp
set(CMAKE_C_STANDARD 11)            # Set the c or cpp language level
set(source_holder "src")            # Set the toplevel source holding folder


project(${project_name})
file(GLOB_RECURSE file_list RELATIVE ${CMAKE_SOURCE_DIR} "${source_holder}/*")


#### Without directory output ####


#foreach( file_path ${file_list} )
#    string( REPLACE ".c" "" new_name ${file_path} )
#    get_filename_component( filename ${new_name} NAME )
#    add_executable( ${filename} ${file_path} )
#endforeach()


##################################


#### With directory output ####

foreach( file_path ${file_list} )

    string( REPLACE ".${lang}" "" new_name ${file_path} )
    get_filename_component( filename ${new_name} NAME )
    get_filename_component( dirname ${new_name} DIRECTORY )
    string( REPLACE "${source_holder}" "" source_without_src ${dirname} )
    set( CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/${source_without_src}" )

    #message( ${source_without_src} )   # For the output control

    add_executable( ${filename} ${file_path} )
endforeach()