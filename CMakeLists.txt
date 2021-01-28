cmake_minimum_required(VERSION 3.17)
project(HelloWorldWithDearImGui)

#-----------------------------------------------------------------------------------------------------------------------
# Download dependencies for GitHub
include(FetchContent)

FetchContent_Declare(
        glew
        GIT_REPOSITORY https://github.com/Perlmint/glew-cmake.git
        GIT_TAG glew-cmake-2.2.0
)

FetchContent_Declare(
        glfw
        GIT_REPOSITORY https://github.com/glfw/glfw
        GIT_TAG 3.3.2
        EXCLUDE_FROM_ALL
)

FetchContent_Declare(
        imgui
        GIT_REPOSITORY https://github.com/ocornut/imgui
        GIT_TAG v1.80
)

FetchContent_MakeAvailable(glew glfw imgui)

set_property(DIRECTORY ${glew_SOURCE_DIR} PROPERTY EXCLUDE_FROM_ALL YES)
set_property(DIRECTORY ${glfw_SOURCE_DIR} PROPERTY EXCLUDE_FROM_ALL YES)

#-----------------------------------------------------------------------------------------------------------------------
# Configure C++ version

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

#-----------------------------------------------------------------------------------------------------------------------
# Create executable
set(EXECUTABLE_NAME ${PROJECT_NAME})

add_executable(${EXECUTABLE_NAME}
        main.cpp

        ${imgui_SOURCE_DIR}/imgui.cpp
        ${imgui_SOURCE_DIR}/imgui.h
        ${imgui_SOURCE_DIR}/imgui_demo.cpp
        ${imgui_SOURCE_DIR}/imgui_draw.cpp
        ${imgui_SOURCE_DIR}/imgui_internal.h
        ${imgui_SOURCE_DIR}/imgui_tables.cpp
        ${imgui_SOURCE_DIR}/imgui_widgets.cpp

        ${imgui_SOURCE_DIR}/backends/imgui_impl_glfw.cpp
        ${imgui_SOURCE_DIR}/backends/imgui_impl_opengl3.cpp
        )

# Add options for warning
if (CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    target_compile_options(${EXECUTABLE_NAME}
            PRIVATE
            -Wall -Wextra -pedantic
            )
endif ()

# Add a define to use the static version of Glew
target_compile_definitions(${EXECUTABLE_NAME}
        PRIVATE
        GLEW_STATIC
        )

# Set the include path
target_include_directories(${EXECUTABLE_NAME}
        PRIVATE
        ${imgui_SOURCE_DIR}/
        )

# Link against the appropriate libraries
target_link_libraries(${EXECUTABLE_NAME}
        PRIVATE
        glfw
        libglew_static

        $<$<CXX_COMPILER_ID:GNU>:opengl32.a>
        $<$<CXX_COMPILER_ID:MSVC>:opengl32.lib>
        )