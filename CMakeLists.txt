cmake_minimum_required(VERSION 3.0)

project(stb)

if (STB_ALL)
  set(STB_IMAGE 1)
endif (STB_ALL)

if (STB_IMAGE)
  set(STB_IMAGE_LIB stb_image)
  add_library("${STB_IMAGE_LIB}" stb_image.cpp)
  set(CPACK_GENERATOR "ZIP")
  install(TARGETS "${STB_IMAGE_LIB}" DESTINATION lib)
  install(FILES stb_image.h DESTINATION include/stb)
  install(FILES stb_image_write.h DESTINATION include/stb)

  add_definitions(-DSTB_IMAGE=1)
endif(STB_IMAGE)

include(CPack)
