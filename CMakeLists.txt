cmake_minimum_required(VERSION 3.15)
project(serial CXX)

# ==============================================
# Dependencies

# ==============================================
# Targets

add_library(serial 
    "src/serial.cc"
    "src/impl/unix.cc"
    "src/impl/list_ports/list_ports_linux.cc"
)

target_include_directories(serial 
PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

target_link_libraries( serial
INTERFACE
    rt
    pthread
)

target_compile_options(serial 
PUBLIC
  -Wall 
  -Wextra 
  -Wpedantic
)

target_compile_features(serial
PUBLIC
  cxx_std_17
)

# ==============================================
# Install

install(
  DIRECTORY include/
  DESTINATION include
  PATTERN "impl" EXCLUDE
)

install(
  TARGETS serial
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
)