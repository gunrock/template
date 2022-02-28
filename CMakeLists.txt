# Installing correct cmake version is easy!
# 1) Find the respective version here;
# https://github.com/Kitware/CMake/releases,
# and 2) replace the [x.xx.x] in the following
# commands with the version number (remove the
# brackets). For example, if you are installing
# CMake 3.22.1, replace [x.xx.x] with 3.22.1:

# wget https://github.com/Kitware/CMake/releases/download/v[x.xx.x]/cmake-[x.xx.x]-linux-x86_64.sh
# chmod +x ./cmake-[x.xx.x]-linux-x86_64.sh
# ./cmake-[x.xx.x]-linux-x86_64.sh
# sudo mv cmake-[x.xx.x]-linux-x86_64 /opt/cmake
# sudo ln -s /opt/cmake/bin/* /usr/local/bin/
cmake_minimum_required(VERSION 3.20.1 FATAL_ERROR)

# Project name.
project(my_application
  LANGUAGES CXX C CUDA
)

# Dependencies directory.
set(PROJECT_DEPS_DIR externals)
set(ESSENTIALS_BUILD_EXAMPLES OFF)

# CMake modules.
include(${PROJECT_SOURCE_DIR}/cmake/FetchEssentials.cmake)

# Add executables.
add_library(${PROJECT_NAME} SHARED 
    ${CMAKE_CURRENT_SOURCE_DIR}/src/hello.cu
)

# Include directories.
target_include_directories(${PROJECT_NAME}
    PUBLIC ${ESSENTIALS_INCLUDE_DIR}
)

# Link with the libraries.
target_link_libraries(${PROJECT_NAME}
    PUBLIC essentials
)

# Correct location of the outputs.
set_target_properties(${PROJECT_NAME}
    PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)

# Install the library.
install(TARGETS ${PROJECT_NAME})

# Add individual executables (programs).
add_executable(hello ${CMAKE_CURRENT_SOURCE_DIR}/src/hello.cu)
target_link_libraries(hello
  PRIVATE ${PROJECT_NAME}
)

# Correct location of the executables.
set_target_properties(hello
    PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)