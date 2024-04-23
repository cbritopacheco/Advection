cmake_minimum_required(VERSION 3.12)

project(Advection C)

# ---- Configure compiler ----------------------------------------------------
add_compile_options(
  -g
  -O0
  -Wall
  -Wextra
  -Wpedantic
  -Wno-newline-eof
  -Wno-missing-braces
  -Wno-char-subscripts
  -Wno-unused-variable
  -Wno-unused-function
  -Wno-unused-parameter
  -Wno-sign-compare
  -Wno-incompatible-function-pointer-types)

# ---- ISCD::Commons ---------------------------------------------------------
add_subdirectory(
  ${PROJECT_SOURCE_DIR}/third-party/ISCD/Commons
  ${PROJECT_BINARY_DIR}/third-party/ISCD/Commons)
target_include_directories(Commons
  INTERFACE
  ${PROJECT_SOURCE_DIR}/third-party/ISCD/Commons/sources)
add_library(ISCD::Commons ALIAS Commons)

# ---- Executable ------------------------------------------------------------
file(GLOB_RECURSE Advection_SRCS sources/*.c)
file(GLOB_RECURSE Advection_HEADERS sources/*.h)

add_executable(Advection ${Advection_SRCS} ${Advection_HEADERS})

target_link_libraries(Advection
  PRIVATE
  m
  pthread
  ISCD::Commons)
