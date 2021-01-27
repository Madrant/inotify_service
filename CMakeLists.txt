# Check minimum required CMake version
cmake_minimum_required(VERSION 3.7)

# Set project name (package name, source archive name)
project("inotify-service")

# Check cmake directories
message("Source dir: ${CMAKE_SOURCE_DIR}")
message("Binary dir: ${CMAKE_BINARY_DIR}")

if("${CMAKE_SOURCE_DIR}" STREQUAL "${CMAKE_BINARY_DIR}")
    message(FATAL_ERROR "cmake in-source build are not allowed - please call cmake from 'build' directory")
endif()

install(
    FILES inotify-service
    PERMISSIONS OWNER_EXECUTE OWNER_WRITE OWNER_READ GROUP_EXECUTE GROUP_READ WORLD_EXECUTE WORLD_READ
    DESTINATION /usr/local/bin
)

# Packaging (make package, make package_source)
set(CPACK_GENERATOR "DEB")

set(CPACK_DEBIAN_PACKAGE_MAINTAINER "Aleksey Polygaev, Tver") #required

set(PACKAGE_VERSION "1.0.0")
set(CPACK_PACKAGE_VERSION "${PACKAGE_VERSION}")
set(CPACK_PACKAGE_VERSION_MAJOR 1)
set(CPACK_PACKAGE_VERSION_MINOR 0)
set(CPACK_PACKAGE_VERSION_PATCH 0)

set(CPACK_DEBIAN_FILE_NAME "inotify-service-${PACKAGE_VERSION}.deb")

include(CPack)
