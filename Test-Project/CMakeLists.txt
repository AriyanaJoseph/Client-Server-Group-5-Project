# CMakeList.txt : CMake project for ClientProject, include source and define
# project specific logic here.
cmake_minimum_required (VERSION 3.16)

# Set the project name.
project ("Test-Project" CXX)

# CPP Only
enable_language(CXX)

# specify the C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)
IF (WIN32)
    link_libraries(ws2_32 wsock32)
ENDIF()

# Add source to this project's executable.
add_executable (BasicTest "BasicTest.cpp")

# Tests and install targets if needed.
include(CTest)
add_test(first_and_only_test BasicTest)

include(FetchContent)
FetchContent_Declare(
  googletest
  URL https://github.com/google/googletest/archive/609281088cfefc76f9d0ce82e1ff6c30cc3591e5.zip
)

# For Windows: Prevent overriding the parent project's compiler/linker settings
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

enable_testing()

target_link_libraries(
  BasicTest
  gtest_main
)

include(GoogleTest)
gtest_discover_tests(BasicTest)
