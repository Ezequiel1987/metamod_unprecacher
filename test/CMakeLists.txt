cmake_minimum_required(VERSION 2.8)
project(tester)
set(CMAKE_INCLUDE_PATH "${CMAKE_CURRENT_SOURCE_DIR}")

find_package(CxxTest REQUIRED)
#cmake_policy(SET CMP0040 NEW)

if(CXXTEST_FOUND)
enable_testing()
file(GLOB_RECURSE TESTES ${CMAKE_CURRENT_SOURCE_DIR}/*.h ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
CXXTEST_ADD_TEST(${PROJECT_NAME} runner.cpp ${TESTES})
target_link_libraries(${PROJECT_NAME} unprecacher_static)
target_compile_features(${PROJECT_NAME} PRIVATE cxx_range_for)
set_target_properties(${PROJECT_NAME} PROPERTIES COMPILE_FLAGS "-m32" LINK_FLAGS "-m32")

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD COMMAND ./${PROJECT_NAME})
endif()
