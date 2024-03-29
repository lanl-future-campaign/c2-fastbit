cmake_minimum_required(VERSION 3.5)
project(c2_fastbit C CXX)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build." FORCE)
    set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS
            "Debug" "Release" "RelWithDebInfo" "MinSizeRel")
endif()
mark_as_advanced(CLEAR CMAKE_EXE_LINKER_FLAGS)
set(BUILD_SHARED_LIBS "OFF" CACHE BOOL "Build a shared library")
set(FASTBIT_CXX_STANDARD "11" CACHE STRING "C++ std to probe")
set(FASTBIT_CXX_STANDARD_REQUIRED "OFF" CACHE BOOL "C++ std must be met")
set(FASTBIT_USE_CXX_ATOMIC "ON" CACHE BOOL "Use C++ <atomic>")
mark_as_advanced(FASTBIT_CXX_STANDARD FASTBIT_CXX_STANDARD_REQUIRED)
set_property(CACHE FASTBIT_CXX_STANDARD PROPERTY STRINGS "98" "11")
set(CMAKE_CXX_STANDARD ${FASTBIT_CXX_STANDARD})
set(CMAKE_CXX_STANDARD_REQUIRED ${FASTBIT_CXX_STANDARD_REQUIRED})

# link shared lib with full rpath. on some modern platforms, the newer
# runpath will be used instead of rpath.
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)
# quiet CMP0042 warning  (not needed if cmake >=3.0)
set(CMAKE_MACOSX_RPATH 1)

add_subdirectory(src)
add_subdirectory(examples)
