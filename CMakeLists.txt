cmake_minimum_required(VERSION 3.0)

project(STBImage)

add_definitions(-DSTB_IMAGE=1)
set(LIB_NAME "stb_image")
add_library("${LIB_NAME}" stb_image.cpp)
SET(CPACK_PACKAGE_VERSION_MAJOR 2)
SET(CPACK_PACKAGE_VERSION_MINOR 0)
SET(CPACK_PACKAGE_VERSION_PATCH 0)
set(STB_IMAGE_VERSION "${CPACK_PACKAGE_VERSION_MAJOR}.${CPACK_PACKAGE_VERSION_MINOR}.${CPACK_PACKAGE_VERSION_PATCH}")

set(CPACK_GENERATOR "ZIP")

if (WIN32)
    SET(CPACK_SYSTEM_NAME "Windows")
endif (WIN32)

# Install library and headers
install(TARGETS "${LIB_NAME}"
    EXPORT stb_targets
    DESTINATION lib
)
install(FILES stb_image.h
    DESTINATION include/stb
    COMPONENT Devel
)
install(FILES stb_image_write.h
    DESTINATION include/stb
    COMPONENT Devel
)
# Install library and headers


# Create cmake files for import
export(EXPORT stb_targets
    FILE STBImageTargets.cmake
)

install(EXPORT stb_targets
    FILE "STBImageTargets.cmake"
    DESTINATION lib/cmake
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/STBImageConfigVersion.cmake"
    VERSION "${STB_IMAGE_VERSION}"
    COMPATIBILITY AnyNewerVersion
)
configure_file("${CMAKE_SOURCE_DIR}/cmake/STBImageConfig.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/STBImageConfig.cmake"
    COPYONLY
)

install(
    FILES
    cmake/STBImageConfig.cmake
    "${CMAKE_CURRENT_BINARY_DIR}/STBImageConfigVersion.cmake"
    DESTINATION lib/cmake
    COMPONENT Devel
)

install(
    FILES
    cmake/STBImageIncludes.cmake
    DESTINATION lib/cmake
    COMPONENT Devel
)
# Create cmake files for import

include(CPack)
