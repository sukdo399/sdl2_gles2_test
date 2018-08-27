cmake_minimum_required(VERSION 2.8.7)
project(GLES2 C CXX)

# ---
# add include files
include_directories(${CMAKE_SOURCE_DIR})
include_directories(${CMAKE_SOURCE_DIR}/src)
include_directories(${CMAKE_SOURCE_DIR}/include)

# ---
# find required packages
include(FindPkgConfig)

pkg_check_modules(SDL2 REQUIRED sdl2)
include_directories(${SDL2_INCLUDE_DIRS})

pkg_check_modules(GLES2.0 REQUIRED glesv2)
include_directories(${GLES2.0_INCLUDE_DIRS})

MESSAGE( "CMAKE_SOURCE_DIR: " ${CMAKE_SOURCE_DIR})

# ---
# create executable file
set(BIN_NAME GLES2)

file(GLOB SOURCES ${CMAKE_SOURCE_DIR}/src/*.c)
set(SRC_LIST
    ${SOURCES}
)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/result/")
add_executable(${BIN_NAME} ${SRC_LIST})
set_target_properties(${BIN_NAME} PROPERTIES LINKER_LANGUAGE C)

target_link_libraries (${BIN_NAME}
        ${SDL2_LDFLAGS}
        ${GLES2.0_LDFLAGS}
        m
)

