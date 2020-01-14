cmake_minimum_required(VERSION 3.5.1)
project(ua-parser-lib-builder LANGUAGES CXX)

add_subdirectory(contrib/re2)

set(RE2_HEADERS contrib/re2)

set(BUILD_SHARED_LIBS OFF)
add_subdirectory(contrib/yaml-cpp)

set(YAML-CPP_HEADERS contrib/yaml-cpp/include)

include_directories(BEFORE ${RE2_HEADERS})
include_directories(BEFORE ${YAML-CPP_HEADERS})

SET(EXT_CXX_FLAGS " -std=c++0x -Wall -Werror -g -fPIC -O3")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${EXT_CXX_FLAGS}")

add_library(uaparser_cpp STATIC
    contrib/uap-cpp/UaParser.cpp
    contrib/uap-cpp/internal/Pattern.cpp
    contrib/uap-cpp/internal/AlternativeExpander.cpp
    contrib/uap-cpp/internal/SnippetIndex.cpp
    contrib/uap-cpp/internal/ReplaceTemplate.cpp
)

target_link_libraries(uaparser_cpp PRIVATE
    re2 yaml-cpp 
)

get_directory_property(hasParent PARENT_DIRECTORY)
set(uaparser_cpp_INCLUDE_DIR contrib/uap-cpp)
if(hasParent)
    set(uaparser_cpp_INCLUDE_DIR ${uaparser_cpp_INCLUDE_DIR} PARENT_SCOPE)
endif()

