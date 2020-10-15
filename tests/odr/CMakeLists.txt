file(GLOB_RECURSE FOUND_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/../../include/*.hpp")
list(TRANSFORM FOUND_HEADERS REPLACE ".*/include/" "")
list(FILTER FOUND_HEADERS EXCLUDE REGEX ".*dnsa_connection.*")

foreach(header_file ${FOUND_HEADERS})
  string(REGEX REPLACE "[/\\]" "-" source_file ${header_file})
  get_filename_component(source_file ${source_file} NAME_WE)
  configure_file(${CMAKE_CURRENT_SOURCE_DIR}/odr.tmpl
                 ${CMAKE_CURRENT_BINARY_DIR}/${source_file}.1.odr.cpp)
  configure_file(${CMAKE_CURRENT_SOURCE_DIR}/odr.tmpl
                 ${CMAKE_CURRENT_BINARY_DIR}/${source_file}.2.odr.cpp)
endforeach()

file(GLOB FOUND_ODR_SOURCES "${CMAKE_CURRENT_BINARY_DIR}/*.cpp")

add_library(test_odr SHARED ${FOUND_ODR_SOURCES})
setup_test(test_odr)
