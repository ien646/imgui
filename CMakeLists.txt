project(imgui LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

option(IMGUI_OPENGL3 "Use opengl3 impl" ON)
option(IMGUI_GLFW "Use glfw impl" ON)
option(IMGUI_GLAD "Use along glad loader" ON)

add_library(imgui
    imgui.cpp
    imgui_demo.cpp
    imgui_draw.cpp
    imgui_widgets.cpp
    misc/cpp/imgui_stdlib.cpp
)

if(IMGUI_OPENGL3)
    target_sources(imgui PUBLIC "examples/imgui_impl_opengl3.cpp")
    target_include_directories(imgui PUBLIC "examples")
endif()

if(IMGUI_GLFW)
    target_sources(imgui PUBLIC "examples/imgui_impl_glfw.cpp")
    target_include_directories(imgui PUBLIC "examples")
    target_link_libraries(imgui PUBLIC glfw)
endif()

if(IMGUI_GLAD)
    target_link_libraries(imgui PUBLIC glad)
endif()

target_include_directories(imgui PUBLIC .)
