cmake_minimum_required(VERSION 3.18)
project(RaylibGames CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(POLICY CMP0135)
    cmake_policy(SET CMP0135 NEW)
endif()

# Fix for Raylib needing CMake 3.0 on CMake 4+
set(CMAKE_POLICY_VERSION_MINIMUM "3.0.0" CACHE STRING "" FORCE)

# ── Raylib (assumed installed or provided as submodule) ───────────────────
find_package(raylib QUIET)
if (NOT raylib_FOUND)
    include(FetchContent)
    FetchContent_Declare(
        raylib
        URL https://github.com/raysan5/raylib/archive/refs/tags/5.0.zip
    )
    FetchContent_MakeAvailable(raylib)
endif()

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

# ── Pong ──────────────────────────────────────────────────────────────────
add_executable(pong pong.cpp)
target_link_libraries(pong PRIVATE raylib)
target_compile_options(pong PRIVATE -Wall -Wextra -O2)

# ── Tetris ────────────────────────────────────────────────────────────────
add_executable(tetris tetris.cpp)
target_link_libraries(tetris PRIVATE raylib)
target_compile_options(tetris PRIVATE -Wall -Wextra -O2)
