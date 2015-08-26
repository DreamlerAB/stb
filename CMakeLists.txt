cmake_minimum_required(VERSION 3.0)

project(stb)

if (STB_ALL)
    set(STB_IMAGE 1)
endif (STB_ALL)

if (STB_IMAGE)
    set(STB_IMAGE_LIB stb_image)
    add_definitions(-DSTB_IMAGE=1)
    add_library("${STB_IMAGE_LIB}" stb_image.cpp)
    SET(CPACK_PACKAGE_VERSION_MAJOR 2)
    SET(CPACK_PACKAGE_VERSION_MINOR 0)
    SET(CPACK_PACKAGE_VERSION_PATCH 0)

    set(CPACK_GENERATOR "ZIP")

    if (WIN32)
        SET(CPACK_SYSTEM_NAME "Windows")
    endif (WIN32)

    install(FILES stb_image.h DESTINATION include/stb)
    install(FILES stb_image_write.h DESTINATION include/stb)
    install(TARGETS "${STB_IMAGE_LIB}" DESTINATION lib)
endif(STB_IMAGE)

include(CPack)
