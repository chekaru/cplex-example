cmake_minimum_required(VERSION 2.8.4)
project(cplex_example)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -DIL_STD -m64 -Wall -Werror")
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -Og -ggdb")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -DNDEBUG -O3 -flto")
set(CMAKE_INCLUDE_SYSTEM_FLAG_CXX "-isystem ")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/build")

if(CMAKE_SYSTEM_NAME STREQUAL Darwin)
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -save-temps=obj")
endif()

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
find_package(Cplex)

include_directories("src")
include_directories(SYSTEM ${CPLEX_INCLUDE_DIRS})

set(SOURCE_FILES
    src/graph.h
    src/graph.cpp
    src/solver.h
    src/solver.cpp
    src/main.cpp)

add_executable(cplex_example ${SOURCE_FILES})
target_link_libraries(cplex_example ${CPLEX_LIBRARIES})