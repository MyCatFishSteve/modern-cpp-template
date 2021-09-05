cmake_minimum_required(VERSION 3.21)

# Initialise project
project("Modern C++ Template"
        VERSION 0.1.0.0
        DESCRIPTION "A starting point for my C++ project"
        HOMEPAGE_URL "https://github.com/MyCatFishSteve/modern-cpp-template"
        LANGUAGES "CXX")

list(APPEND CMAKE_MODULE_PATH "${CMAKE_BINARY_DIR}")
list(APPEND CMAKE_PREFIX_PATH "${CMAKE_BINARY_DIR}")

# Download the CMake wrapper for Conan C and C++ package manager
if(NOT EXISTS "${CMAKE_BINARY_DIR}/conan.cmake")
    file(DOWNLOAD "https://raw.githubusercontent.com/conan-io/cmake-conan/v0.16.1/conan.cmake" "${CMAKE_BINARY_DIR}/conan.cmake"
        EXPECTED_HASH "SHA256=396e16d0f5eabdc6a14afddbcfff62a54a7ee75c6da23f32f7a31bc85db23484"
        TLS_VERIFY ON)
endif()

# Execute CMake wrapper
include("${CMAKE_BINARY_DIR}/conan.cmake")

conan_check(VERSION 1.39.0 REQUIRED)

# Add Conan remote 
# conan_add_remote(NAME "bincrafters" URL "https://bincrafters.jfrog.io/artifactory/api/conan/public-conan")

conan_cmake_configure(REQUIRES fmt/8.0.0
                      GENERATORS cmake_find_package)

conan_cmake_autodetect(settings)

conan_cmake_install(PATH_OR_REFERENCE .
                    BUILD missing
                    SETTINGS ${settings})

find_package("fmt")

add_subdirectory("Source")
