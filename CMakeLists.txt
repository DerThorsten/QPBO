cmake_minimum_required (VERSION 2.8)
project (QPBO)


# default build-type (release)
IF(DEFINED CMAKE_BUILD_TYPE)
   SET(CMAKE_BUILD_TYPE ${CMAKE_BUILD_TYPE} CACHE STRING "Choose the type of build, options are: None(CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel.")
ELSE()
   SET(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build, options are: None(CMAKE_CXX_FLAGS or CMAKE_C_FLAGS used) Debug Release RelWithDebInfo MinSizeRel.")
ENDIF()


set(${PROJECT_NAME}_VERSION_MAJOR 1)
set(${PROJECT_NAME}_VERSION_MINOR 4)
set(${PROJECT_NAME}_VERSION_PATCH 21)


set(${PROJECT_NAME}_VERSION 
    ${${PROJECT_NAME}_VERSION_MAJOR}.${${PROJECT_NAME}_VERSION_MINOR}.${${PROJECT_NAME}_VERSION_PATCH}
)





include(GNUInstallDirs)
include(CMakePackageConfigHelpers)


install(FILES include/qpbo/qpbo.hpp
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/qpbo)


set(QPBO_CMAKECONFIG_INSTALL_DIR "${CMAKE_INSTALL_LIBDIR}/cmake/QPBO" CACHE
    STRING "install path for QPBOConfig.cmake")

configure_package_config_file(QPBOConfig.cmake.in
                              "${CMAKE_CURRENT_BINARY_DIR}/QPBOConfig.cmake"
                              INSTALL_DESTINATION ${QPBO_CMAKECONFIG_INSTALL_DIR})


write_basic_package_version_file(${CMAKE_CURRENT_BINARY_DIR}/QPBOConfigVersion.cmake
                                 VERSION ${QPBO_VERSION}
                                 COMPATIBILITY AnyNewerVersion)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/QPBOConfig.cmake
              ${CMAKE_CURRENT_BINARY_DIR}/QPBOConfigVersion.cmake
        DESTINATION ${QPBO_CMAKECONFIG_INSTALL_DIR})
