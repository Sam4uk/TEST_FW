cmake_minimum_required(VERSION 3.0)

project(GTESTING)

enable_testing()

set(TEST_NAME MY_TEST)

find_package(GTest REQUIRED)

include_directories( ${GTEST_INCLUDE_DIRS})

add_executable(
    ${PROJECT_NAME} 
    main.cpp
    )

add_executable(
    ${TEST_NAME}
    test.cpp
    )


target_link_libraries(
    ${TEST_NAME} 
    ${GTEST_LIBRARIES}
    ${GTEST_MAIN_LIBRARIES}
    pthread
    )

add_test(
    NAME ${TEST_NAME}
    COMMAND ${TEST_NAME}
)