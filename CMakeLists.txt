cmake_minimum_required(VERSION 3.15)
project(woodall_serial CXX)

# ==============================================
# Dependencies

# ==============================================
# Targets

add_library(woodall_serial 
    "src/serial.cc"
    "src/impl/unix.cc"
    "src/impl/list_ports/list_ports_linux.cc"
)

target_include_directories(woodall_serial 
PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

target_link_libraries( woodall_serial
INTERFACE
    rt
    pthread
)

target_compile_options(woodall_serial 
PUBLIC
  -Wall 
  -Wextra 
  -Wpedantic
)

target_compile_features(woodall_serial
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
  TARGETS woodall_serial
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
)