#
# This file is a part of the Sharemind framework.
# Copyright (C) Cybernetica AS
#
# All rights are reserved. Reproduction in whole or part is prohibited
# without the written consent of the copyright owner. The usage of this
# code is subject to the appropriate license agreement.
#
CMAKE_MINIMUM_REQUIRED(VERSION "3.0")
PROJECT(SharemindDataStoreApi VERSION "0.1.0" LANGUAGES "CXX")

INCLUDE("${CMAKE_CURRENT_SOURCE_DIR}/config.local" OPTIONAL)
INCLUDE("${CMAKE_CURRENT_BINARY_DIR}/config.local" OPTIONAL)

FIND_PACKAGE(SharemindCMakeHelpers 1.6 REQUIRED)


# Data Store API headers:
FILE(GLOB SharemindDataStoreApi_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.h")
INSTALL(FILES ${SharemindDataStoreApi_HEADERS}
        DESTINATION "include/sharemind/"
        COMPONENT "dev")
SharemindAddInterfaceLibrary(DataStoreApi
    EXPOSE_FILES ${SharemindDataStoreApi_HEADERS})
TARGET_INCLUDE_DIRECTORIES(DataStoreApi
    INTERFACE
        # $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src> # TODO
        $<INSTALL_INTERFACE:include>
    )
SharemindCreateCMakeFindFilesForTarget(DataStoreApi)


# Packaging:
SharemindSetupPackaging()
SharemindAddComponentPackage("dev"
    NAME "libsharemind-data-store-api-dev"
    DESCRIPTION "Sharemind Data Store API development headers"
    DEB_SECTION "libdevel"
)
SharemindPackagingFinalize()
