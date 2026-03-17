cmake_minimum_required(VERSION 3.24)
project(LuaBench)

add_custom_command(OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/long.cnf
    COMMAND cp ${CMAKE_CURRENT_SOURCE_DIR}/long.cnf ${CMAKE_CURRENT_BINARY_DIR}
    COMMAND cp ${CMAKE_CURRENT_SOURCE_DIR}/run.sh ${CMAKE_CURRENT_BINARY_DIR}
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR})
add_custom_target(minisat_input SOURCES ${CMAKE_CURRENT_BINARY_DIR}/long.cnf ${CMAKE_CURRENT_SOURCE_DIR}/run.sh)
add_executable(minisat Main.cpp Solver.cpp)
target_link_libraries(minisat m)
add_dependencies(minisat minisat_input)