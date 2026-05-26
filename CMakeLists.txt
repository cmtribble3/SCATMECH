cmake_minimum_required(VERSION 3.16)

project(SCATMECH LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

file(GLOB SCATMECH_SOURCES CONFIGURE_DEPENDS
    "${CMAKE_CURRENT_SOURCE_DIR}/code/*.cpp"
)

add_library(scatmech STATIC ${SCATMECH_SOURCES})
target_include_directories(scatmech PUBLIC
    "${CMAKE_CURRENT_SOURCE_DIR}/code"
)
target_compile_options(scatmech PRIVATE
    -Wno-deprecated-declarations
)

add_executable(BRDFProg code/BRDFProg/BRDFProg.cpp)
target_link_libraries(BRDFProg PRIVATE scatmech m)

add_executable(RCWProg code/RCWProg/RCWProg.cpp)
target_link_libraries(RCWProg PRIVATE scatmech m)

add_executable(ReflectProg code/ReflectProg/ReflectProg.cpp)
target_link_libraries(ReflectProg PRIVATE scatmech m)

add_executable(MieProg code/MieProg/MieProg.cpp)
target_link_libraries(MieProg PRIVATE scatmech m)
