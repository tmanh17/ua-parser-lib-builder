cmake_minimum_required(VERSION 3.5.1)
project(ua-parser-lib-builder LANGUAGES CXX)

add_subdirectory(contrib/re2)

set(RE2_HEADERS
    contrib/re2/re2/filtered_re2.h
    contrib/re2/re2/re2.h
    contrib/re2/re2/set.h
    contrib/re2/re2/stringpiece.h
    )


set(BUILD_SHARED_LIBS OFF)
add_subdirectory(contrib/yaml-cpp)

set(YAML-CPP_HEADERS contrib/yaml-cpp/include)

add_library(uaparser_cpp STATIC
    contrib/uap-cpp/UaParser.cpp
    contrib/uap-cpp/internal/Pattern.cpp
    contrib/uap-cpp/internal/AlternativeExpander.cpp
    contrib/uap-cpp/internal/SnippetIndex.cpp
    contrib/uap-cpp/internal/ReplaceTemplate.cpp
)

target_link_libraries(category_classifier_static PRIVATE
    masks_matcher_static
)

#get_directory_property(hasParent PARENT_DIRECTORY)
#if(hasParent)
#    set(MASK_MATCHER_INCLUDE_DIR ${MASK_MATCHER_INCLUDE_DIR} PARENT_SCOPE)
#    set(CATEGORY_CLASSIFIER_INCLUDE_DIR ${CATEGORY_CLASSIFIER_INCLUDE_DIR} PARENT_SCOPE)
#    set(RapidJSON_INCLUDE_DIR ${RapidJSON_INCLUDE_DIR} PARENT_SCOPE)
#endif()

