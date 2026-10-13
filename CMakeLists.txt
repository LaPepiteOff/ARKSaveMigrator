cmake_minimum_required(VERSION 3.20)

project(ARKSaveMigrator VERSION 0.1.0 LANGUAGES CXX)

configure_file(
    cmake/version.hpp.in
    generated/ark_save_migrator/version.hpp
    @ONLY
)

add_executable(ark_save_migrator src/main.cpp)

target_compile_features(ark_save_migrator PRIVATE cxx_std_20)
set_target_properties(ark_save_migrator PROPERTIES CXX_EXTENSIONS OFF)

target_include_directories(ark_save_migrator PRIVATE
    "${CMAKE_CURRENT_BINARY_DIR}/generated"
)

if(MSVC)
    target_compile_options(ark_save_migrator PRIVATE /W4 /permissive-)
elseif(CMAKE_CXX_COMPILER_ID MATCHES "^(GNU|Clang|AppleClang)$")
    target_compile_options(ark_save_migrator PRIVATE -Wall -Wextra -Wpedantic)
endif()
