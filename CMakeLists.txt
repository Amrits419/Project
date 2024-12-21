cmake_minimum_required(VERSION 3.10)
project(render)

# based largely on: 
# https://github.com/Polytonic/Glitter/blob/master/CMakeLists.txt

# turn off compiler warnings
if(MSVC)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /W4")
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wpedantic -std=c++11")
endif()


# include headers
include_directories("${PROJECT_SOURCE_DIR}/include")
include_directories("${PROJECT_SOURCE_DIR}/dependencies/GLFW")
file(GLOB PROJECT_HEADERS "include/*.h")

# include source files
file(GLOB PROJECT_SOURCES "src/*.cpp")

# group files in IDE
source_group("include" FILES ${PROJECT_HEADERS})
source_group("src" FILES ${PROJECT_SOURCES})


# create the executable
add_executable(render ${PROJECT_SOURCES}
					${PROJECT_HEADERS}) # if not included here, it won't show up in the IDE?
                    
					

# add libraries
target_link_libraries(render 
    "${PROJECT_SOURCE_DIR}/dependencies/lib-universal/libglfw3.a"
    "-framework CoreFoundation"
    "-framework Cocoa"
    "-framework IOKit"
    "-framework CoreVideo"
    "-framework OpenGL")