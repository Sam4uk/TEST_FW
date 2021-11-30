cmake_minimum_required(VERSION 3.0)

project(GTESTING)

enable_testing()

set(TEST_NAME MY_TEST)

configure_file(gitignore.in .gitignore COPYONLY)

include(FetchContent)
FetchContent_Declare(
  googletest
    # Specify the commit you depend on and update it regularly.
    GIT_REPOSITORY https://github.com/google/googletest
    GIT_TAG        e2239ee6043f73722e7aa812a459f54a28552929 # release-1.11.0
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

FetchContent_GetProperties(googletest)
if (NOT googletest_POPULATED)
    FetchContent_Populate(googletest)

    # Perform arbitrary actions on the googletest project

    add_subdirectory(${googletest_SOURCE_DIR} ${googletest_BINARY_DIR})
endif()

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
    gtest_main
    pthread
    )

add_test(
    NAME ${TEST_NAME}
    COMMAND ${TEST_NAME}
)