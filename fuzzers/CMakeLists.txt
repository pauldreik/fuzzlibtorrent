#this is how oss-fuzz passes the fuzzer engine
set(engine $ENV{LIB_FUZZING_ENGINE})

if(NOT EXISTS ${engine}) 
  message(FATAL_ERROR "fuzzing engine ${engine} not found")
endif()

#some glue code to avoid having to repeate the same crappy casts
#over and over again
add_library(glue OBJECT glue/glue.cpp)
target_link_libraries(glue torrent-rasterbar)

#find all fuzzers.
file(GLOB SOURCES "*.cpp")

macro(implement_fuzzer sourcefile)
  get_filename_component(basename ${sourcefile} NAME_WE)
  add_executable(fuzzer_${basename} ${sourcefile})
  target_link_libraries(fuzzer_${basename} torrent-rasterbar)
  target_link_libraries(fuzzer_${basename} glue)
  target_link_libraries(fuzzer_${basename} ${engine})
endmacro()

foreach(X IN ITEMS ${SOURCES})
    implement_fuzzer(${X})
endforeach()

