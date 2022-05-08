cmake_minimum_required(VERSION 3.5)
project(baseencode)

enable_testing()
add_subdirectory(tests)

# set up versioning.
set(BUILD_MAJOR "1")
set(BUILD_MINOR "0")
set(BUILD_VERSION "10")
set(BUILD_VERSION ${BUILD_MAJOR}.${BUILD_MINOR}.${BUILD_VERSION})

set(CMAKE_C_STANDARD 11)
if (MSVC)
    # warning level 4 and all warnings as errors
    #add_compile_options(/W4 /WX)
    add_definitions(-D_CRT_SECURE_NO_WARNINGS=1)
    #add_definitions(-DHAVE_GETOPT_LONG=1)
else()
    # lots of warnings and all warnings as errors
    add_compile_options(-Wunused-result)
endif()
#set(CMAKE_C_FLAGS "-Wall -Werror -fPIC")
set(CMAKE_POSITION_INDEPENDENT_CODE ON) # -fPIC

set(BASEENCODE_HEADERS src/baseencode.h)
set(SOURCE_FILES src/base32.c src/base64.c)

option(BUILD_SHARED_LIBS "Build using shared libraries" OFF)

if(BUILD_SHARED_LIBS)
add_library(${PROJECT_NAME} SHARED ${SOURCE_FILES})
else()
add_library(${PROJECT_NAME} STATIC ${SOURCE_FILES})
endif()
target_link_libraries(${PROJECT_NAME} ${PROJECT_LIBS})
set_target_properties(${PROJECT_NAME} PROPERTIES VERSION ${BUILD_VERSION} SOVERSION ${BUILD_MAJOR})

