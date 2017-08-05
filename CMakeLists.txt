cmake_minimum_required(VERSION 2.8.3)
project(libcuckoo_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(ExternalProject)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)

ExternalProject_Add(libcuckoo_src
  GIT_REPOSITORY https://github.com/efficient/libcuckoo.git
  GIT_TAG 916590f3fc2e983cf122e977e6975fdbb8eb11c2
  UPDATE_COMMAND ""
  CMAKE_ARGS -DCMAKE_INSTALL_PREFIX:PATH=${CATKIN_DEVEL_PREFIX}
  -DCMAKE_BUILD_TYPE:STRING=Release
)

cs_add_library(${PROJECT_NAME} src/dependency_tracker.cc)
add_dependencies(${PROJECT_NAME} libcuckoo_src)

cs_install()

cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include
  CFG_EXTRAS libcuckoo-extras.cmake)