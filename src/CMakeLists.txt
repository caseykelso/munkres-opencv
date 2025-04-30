cmake_minimum_required (VERSION 3.20)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)  # Use -std=c++20 instead of -std=gnu++20
set(BUILD_SHARED_LIBS ON)

project(munkres)

find_package(OpenCV REQUIRED)

add_executable(munkres_test main.cpp)

add_library(munkres SHARED munkres.cpp)

include_directories(BEFORE ${OpenCV_INCLUDE_DIRS} ${CMAKE_PREFIX_PATH}/include ${CMAKE_CURRENT_SOURCE_DIR})

target_link_directories(munkres BEFORE PUBLIC ${CMAKE_PREFIX_PATH}/lib)
target_link_directories(munkres_test BEFORE PUBLIC ${CMAKE_PREFIX_PATH}/lib)
target_link_libraries(munkres_test munkres ${OpenCV_LIBS} pthread rt)

install(FILES munkres.h DESTINATION include)
install(TARGETS munkres DESTINATION lib)
install(TARGETS munkres_test DESTINATION bin)

