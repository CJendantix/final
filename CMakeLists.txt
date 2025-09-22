cmake_minimum_required(VERSION 3.16)
project(TICTACTOE VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20 CACHE STRING "C++ standard to use")
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

option(CMAKE_EXPORT_COMPILE_COMMANDS "Generate compile_commands.json" ON)

file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")

add_executable(TICTACTOE ${SOURCES})
target_include_directories(TICTACTOE PRIVATE src)

include(FetchContent)

# FTXUI
FetchContent_Declare(
    ftxui
    GIT_REPOSITORY https://github.com/ArthurSonzogni/ftxui.git
    GIT_TAG v5.0.0
    GIT_SHALLOW TRUE
)
FetchContent_MakeAvailable(ftxui)
target_link_libraries(TICTACTOE PRIVATE ftxui::dom ftxui::screen ftxui::component)

# cxxopts (header-only)
FetchContent_Declare(
    cxxopts
    GIT_REPOSITORY https://github.com/jarro2783/cxxopts.git
    GIT_TAG v3.3.1
)
FetchContent_MakeAvailable(cxxopts)
target_include_directories(TICTACTOE PRIVATE ${cxxopts_SOURCE_DIR}/include)
