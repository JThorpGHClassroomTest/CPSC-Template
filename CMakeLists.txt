cmake_minimum_required(VERSION 3.30.0)
project(Project LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Dirs
add_subdirectory(include)
add_subdirectory(src)

# Executable
add_executable(${PROJECT_NAME} "src/main.cpp")
target_link_libraries(${PROJECT_NAME} include)
target_link_libraries(${PROJECT_NAME} src)

# Test Executables
add_executable(test1 "tests/test1.cpp")
target_link_libraries(test1 include)
target_link_libraries(test1 src)

# Test Run Commands
ADD_CUSTOM_TARGET(run_test1
    COMMENT "Running Test 1..."
    COMMAND $<TARGET_FILE:test1>
    USES_TERMINAL
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    DEPENDS test1
)
