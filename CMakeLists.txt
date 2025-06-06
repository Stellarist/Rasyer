cmake_minimum_required(VERSION 3.20)

project(SRenderer)

add_compile_definitions(PROJECT_PATH="${CMAKE_SOURCE_DIR}")
add_compile_definitions(BUILD_RPATH="${CMAKE_BINARY_DIR}")

file(GLOB_RECURSE RS_INC_LIST src/rasterizer/*.hpp)
file(GLOB_RECURSE RS_SRC_LIST src/rasterizer/*.cpp)
file(GLOB_RECURSE RT_INC_LIST src/raytracer/*.hpp)
file(GLOB_RECURSE RT_SRC_LIST src/raytracer/*.cpp)

source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR}/src/rasterizer PREFIX "Header Files/Rasterizer" FILES ${RS_INC_LIST})
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR}/src/rasterizer PREFIX "Source Files/Rasterizer" FILES ${RS_SRC_LIST})
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR}/src/raytracer PREFIX "Header Files/Raytracer" FILES ${RT_INC_LIST})
source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR}/src/raytracer PREFIX "Source Files/Raytracer" FILES ${RT_SRC_LIST})

find_package(glad REQUIRED)
find_package(glfw3 REQUIRED)
find_package(Eigen3 REQUIRED)
find_package(Stb REQUIRED)
find_package(tinyobjloader REQUIRED)

add_executable(rasterizer 
    ${RS_INC_LIST} 
    ${RS_SRC_LIST}
)

target_link_libraries(rasterizer
    glfw
    glad::glad
    Eigen3::Eigen
    tinyobjloader::tinyobjloader
    ${STB_LIBRARIES}
)

add_executable(raytracer
    ${RT_INC_LIST} 
    ${RT_SRC_LIST}
)

target_link_libraries(raytracer
    Eigen3::Eigen
    tinyobjloader::tinyobjloader
    ${STB_LIBRARIES}
)

