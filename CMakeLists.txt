cmake_minimum_required(VERSION 2.8)
project(facebook-tunnel)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")
set(CMAKE_CXX_FLAGS "-std=c++0x")
find_package(CURL)
find_package(gumbo)
find_package (Threads)
add_library(tun_dev tun_dev.c)
add_library(facebook facebook.cpp)
add_library(tun	tun.cpp)
add_library(base64encode base64encode.c)
target_link_libraries(tun tun_dev base64encode)
add_library(client client.cpp)
add_library(utils utils.cpp)
add_executable(facebook-tunnel main.cpp)
target_link_libraries(facebook-tunnel base64encode tun client facebook utils ${CURL_LIBRARY} ${GUMBO_LIBRARY} ${CMAKE_THREAD_LIBS_INIT})
