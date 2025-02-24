cmake_minimum_required(VERSION 3.0.0)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

add_definitions(-w)

set(PROJECT GDMenu)
project(${PROJECT})

file(GLOB_RECURSE SOURCE_FILES src/*.cpp src/*.c
     libs/discord_game_sdk/cpp/*.cpp)
add_library(${PROJECT} SHARED ${SOURCE_FILES})

target_include_directories(
  ${PROJECT}
  PRIVATE
    libs/minhook/include
    libs/gd.h/include
    libs/gd.h/
    libs/portaudio/include
    libs/libsndfile/include
    libs/discord_game_sdk/cpp
    libs/cocos-headers/cocos2dx/platform/third_party/win32/curl)

add_subdirectory(libs/minhook)
add_subdirectory(libs/imgui-hook)
add_subdirectory(libs/cocos-headers)
add_subdirectory(libs/fmod-headers)

target_link_libraries(${PROJECT} minhook imgui-hook opengl32 cocos2d fmod)

target_link_libraries(
  ${PROJECT}
  ${CMAKE_SOURCE_DIR}/libs/glew/glew32.lib
  ${CMAKE_SOURCE_DIR}/libs/cocos-headers/cocos2dx/robtop/glfw/glfw3.lib
  ${CMAKE_SOURCE_DIR}/libs/discord_game_sdk/lib/x86/discord_game_sdk.dll.lib
  ${CMAKE_SOURCE_DIR}/libs/portaudio/lib/portaudio_x86.lib
  ${CMAKE_SOURCE_DIR}/libs/libsndfile/lib/sndfile.lib)
