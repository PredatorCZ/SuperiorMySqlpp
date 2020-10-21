cmake_minimum_required(VERSION 3.12)

# TODO: Hardcoded version
project(SuperiorMySqlpp VERSION 0.6.1)

option(TEST_ENABLED "Enable test builds" TRUE)
option(TEST_ODR_ENABLED "Test One Definition Rule" TRUE)
option(TEST_EXTENDED_ENABLED "Enable extended tests" TRUE)
option(GCOV_ENABLED "Enable code coverage." FALSE)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

configure_file(libsuperiormysqlpp.pc.in
               ${CMAKE_CURRENT_BINARY_DIR}/libsuperiormysqlpp.pc @ONLY)

add_subdirectory(src)

if(TEST_ENABLED)
  enable_testing()
  add_subdirectory(tests)
endif()

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/libsuperiormysqlpp.pc
        DESTINATION ${CMAKE_INSTALL_LIBDIR}/pkgconfig)
