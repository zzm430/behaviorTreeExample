cmake_minimum_required(VERSION 3.16)
project(behaviortree)

set(CMAKE_CXX_STANDARD 17)

find_package(Boost COMPONENTS coroutine QUIET)
find_package(Threads)
find_package(Curses QUIET)

list(APPEND BEHAVIOR_TREE_EXTERNAL_LIBRARIES
        ${CMAKE_THREAD_LIBS_INIT}
        ${CMAKE_DL_LIBS}
        ${Boost_LIBRARIES}
        ${CURSES_LIBRARIES} )

include_directories(${CMAKE_SOURCE_DIR}/include)
include_directories(${CMAKE_SOURCE_DIR}/sample_nodes)

list(APPEND NEED_SOURCE
        ${CMAKE_SOURCE_DIR}/src/t01_build_your_first_tree.cpp
        ${CMAKE_SOURCE_DIR}/sample_nodes/dummy_nodes.cpp )

find_library(BT_LIB libbehaviortree_cpp.so HINTS ${CMAKE_SOURCE_DIR}/lib)

add_executable(behaviortree  ${NEED_SOURCE})
target_compile_definitions(behaviortree PRIVATE "MANUAL_STATIC_LINKING")
target_link_libraries(behaviortree ${BT_LIB} ${BEHAVIOR_TREE_EXTERNAL_LIBRARIES} )
