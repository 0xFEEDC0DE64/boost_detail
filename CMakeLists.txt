# Copyright 2018 Peter Dimov
# Copyright 2018 Andrey Semashev
# Distributed under the Boost Software License, Version 1.0.
# See accompanying file LICENSE_1_0.txt or copy at https://www.boost.org/LICENSE_1_0.txt

if(NOT DEFINED IDF_TARGET)

cmake_minimum_required(VERSION 3.5...3.20)

project(boost_detail VERSION "${BOOST_SUPERPROJECT_VERSION}" LANGUAGES CXX)

add_library(boost_detail INTERFACE)
add_library(Boost::detail ALIAS boost_detail)

target_include_directories(boost_detail INTERFACE include)

target_link_libraries(boost_detail
    INTERFACE
        Boost::config
        Boost::core
        Boost::preprocessor
        Boost::static_assert
        Boost::type_traits
)

else()

FILE(GLOB_RECURSE headers include/*.h include/*.hpp)

idf_component_register(
    SRCS
        ${headers}
    INCLUDE_DIRS
        include
    REQUIRES
        boost_config
        boost_core
        boost_preprocessor
        boost_static_assert
        boost_type_traits
)

endif()
