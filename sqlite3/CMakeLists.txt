cmake_minimum_required(VERSION 3.24)
project(ProjectName)

set(CMAKE_C_FLAGS -I.)
set(GeneratedTestInputs ${CMAKE_CURRENT_BINARY_DIR}/test15.sql)

add_custom_command(OUTPUT ${CMAKE_CURRENT_BINARY_DIR}/test15.sql
    COMMAND cp ${CMAKE_CURRENT_SOURCE_DIR}/test*.sql ${CMAKE_CURRENT_BINARY_DIR}
    COMMAND cp ${CMAKE_CURRENT_SOURCE_DIR}/run.sh ${CMAKE_CURRENT_BINARY_DIR}
    COMMAND cp ${CMAKE_CURRENT_SOURCE_DIR}/sqlite3rc ${CMAKE_CURRENT_BINARY_DIR}
    COMMAND cp ${CMAKE_CURRENT_SOURCE_DIR}/commands ${CMAKE_CURRENT_BINARY_DIR}
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    COMMENT "Generating sqlite test inputs")
add_custom_target(sqlite_input SOURCES ${CMAKE_CURRENT_BINARY_DIR}/test15.sql)
add_executable(sqlite3
  sqlite3.c
  shell.c
)
target_compile_definitions(sqlite3 PRIVATE STDC_HEADERS=1 HAVE_SYS_TYPES_H=1 HAVE_SYS_STAT_H=1 HAVE_STDLIB_H=1 HAVE_STRING_H=1 HAVE_MEMORY_H=1 HAVE_STRINGS_H=1 HAVE_INTTYPES_H=1 HAVE_STDINT_H=1 HAVE_UNISTD_H=1 SQLITE_OMIT_LOAD_EXTENSION=1 SQLITE_THREADSAFE=0)
target_include_directories(sqlite3 PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
set_property(TARGET sqlite3 PROPERTY C_STANDARD 17)
add_dependencies(sqlite3 sqlite_input)
