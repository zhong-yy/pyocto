set(CMAKE_CXX_STANDARD 17)

# Platform-specific compiler flags
if(NOT MSVC)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")
endif()

# Enable exception handling for MSVC (required for pybind11)
if(MSVC)
    add_compile_options(/EHsc)
endif()

set(CMAKE_OSX_DEPLOYMENT_TARGET "10.15" CACHE STRING "Minimum macOS deployment target")

include_directories(src)

cmake_minimum_required(VERSION 3.15)
project(_core LANGUAGES CXX)

add_subdirectory(extern/pybind11)
pybind11_add_module(_core
        src/python_bindings.cpp
        src/OctoAssociator.cpp
        src/OctoAssociator.h
        src/types.h
        src/VelocityModel.cpp
        src/VelocityModel.h
        src/types.cpp)

install(TARGETS _core DESTINATION pyocto)
