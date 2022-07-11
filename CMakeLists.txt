cmake_minimum_required(VERSION 3.22.0)
project(libutil CXX)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_CXX_EXTENSIONS ON)
# add non auto includes here
include_directories(${PROJECT_SOURCE_DIR}/Includes)

set(sources src/lib/Math.cpp)

add_library(libutil SHARED ${sources})

if(MSVC)
  target_compile_options(libutil PRIVATE /W4 /WX)
else()
  target_compile_options(libutil PRIVATE -Wall -Wextra -Wpedantic -Werror)
endif()

target_link_libraries(libutil PRIVATE libos) 

set(tests_sources src/tests/Main.cpp)

add_executable(libutilTests ${tests_sources})
target_link_libraries(libutilTests libutil)
