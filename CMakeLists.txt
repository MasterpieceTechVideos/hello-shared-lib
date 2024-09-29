cmake_minimum_required(VERSION 3.5...3.30)

project(hello_world_shared_lib 
    VERSION 1.0.1 
    DESCRIPTION "basic shared library for saying hi :)"
    LANGUAGES CXX
)

add_library(hello_shared_lib SHARED src/hello_shared_lib.cpp) 

set_target_properties(hello_shared_lib PROPERTIES
    VERSION ${PROJECT_VERSION}
    SOVERSION ${PROJECT_VERSION_MAJOR}
    PUBLIC_HEADER ${CMAKE_CURRENT_LIST_DIR}/include/hello_shared_lib.h) 
target_include_directories(hello_shared_lib PRIVATE ${CMAKE_CURRENT_LIST_DIR}/include)

add_custom_command(TARGET hello_shared_lib 
    POST_BUILD COMMAND ${CMAKE_COMMAND} -E 
    copy_if_different ${CMAKE_CURRENT_LIST_DIR}/include/hello_shared_lib.h  
    $<TARGET_FILE_DIR:hello_shared_lib>) 