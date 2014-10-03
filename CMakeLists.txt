cmake_minimum_required (VERSION 2.6)

project (aoladder_contraction)

enable_language(Fortran)


# Setup for gtests.
add_subdirectory(gtest-1.7.0)
enable_testing()
set(INCLUDE_DIRS ${INCLUDE_DIRS} ${gtest_SOURCE_DIR}/include ${gtest_SOURCE_DIR})

# C++11 features are used.
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")


include_directories(${INCLUDE_DIRS})

set(COMMON_FILES
    aoladder_contraction.F;
    lookup_shell.f;
    sip_interface.fh;
    sip_interface.cpp;
    sip_interface.h;
    constants.h;
    imemory.h;
)

# Executable that has hardcoded data from an actual SIALX job.
add_executable(aoladder_contraction_test;
    main.cpp;
    ${COMMON_FILES}
    )

# Gtest executable that generates random data and runs it through aoladder_contraction.
add_executable(gtest_aoladder_contraction;
    main_test.cpp
    constants_data_types.cpp;
    aoladder_contraction_cpp.cpp;
    constants_data_types.h;
    ${COMMON_FILES}
    )

# Link to gtest libraries
target_link_libraries(gtest_aoladder_contraction gtest gtest_main)



