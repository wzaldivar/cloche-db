cmake_minimum_required(VERSION 3.27)
project(cloche_db)

set(CMAKE_CXX_STANDARD 17)

set(BOOST_SRC_DIR "ext/src/boost")
set(BOOST_DEPS_DIR "ext/deps/boost")

if (NOT EXISTS ${PROJECT_SOURCE_DIR}/${BOOST_SRC_DIR}/b2)
    if (UNIX)
        execute_process(COMMAND ./bootstrap.sh --prefix=${PROJECT_SOURCE_DIR}/${BOOST_DEPS_DIR}
                WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}/${BOOST_SRC_DIR})
    endif ()
    if (WIN32)
        execute_process(COMMAND ./bootstrap.bat --prefix=${PROJECT_SOURCE_DIR}/${BOOST_DEPS_DIR}
                WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}/${BOOST_SRC_DIR})
    endif ()
endif ()

if (NOT EXISTS ${PROJECT_SOURCE_DIR}/${BOOST_DEPS_DIR})
    execute_process(COMMAND ./b2 install
            WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}/${BOOST_SRC_DIR})
endif ()

include_directories(ext/deps/boost/include)
link_directories(ext/deps/boost/lib)

add_executable(cloche_db main.cpp)
