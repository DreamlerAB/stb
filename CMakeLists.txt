cmake_minimum_required(VERSION 3.0)

if (STB_ALL)
  set(STB_IMAGE 1)
endif (STB_ALL)

if (STB_IMAGE)
  add_definitions(-DSTB_IMAGE=1)
  add_library(stb_image stb_image.cpp)
endif(STB_IMAGE)
