include(CodeCoverage)
APPEND_COVERAGE_COMPILER_FLAGS()

set(TEST_SRC catch.cpp tests.cpp)
set(TEST_INC inc)

set(TESTS_TARGET "tests")

find_package(Threads)

add_executable(${TESTS_TARGET} ${TEST_SRC})
target_link_libraries(${TESTS_TARGET} qsort ${CMAKE_THREAD_LIBS_INIT})

target_include_directories(${TESTS_TARGET} PRIVATE ${TEST_INC})

target_compile_options(${TESTS_TARGET} PRIVATE -g3 -O0 -coverage -fno-inline -Wno-unused)
set_target_properties(${TESTS_TARGET} PROPERTIES LINK_FLAGS " ${LINK_FLAGS} -coverage")



SETUP_TARGET_FOR_COVERAGE(
     NAME coverage                    # New target name
     EXECUTABLE bin/tests  # Executable in PROJECT_BINARY_DIR
     DEPENDENCIES qsort tests
 )

#target_compile_options(${TESTS_TARGET} PUBLIC -g3 -O0 -fprofile-arcs -ftest-coverage)
#set_target_properties(${TESTS_TARGET} PROPERTIES LINK_FLAGS " ${LINK_FLAGS} -coverage -fprofile-arcs -ftest-coverage")
