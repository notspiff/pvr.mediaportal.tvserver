PROJECT(pvr.mediaportal.tvserver)

CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${PROJECT_SOURCE_DIR})

ENABLE_LANGUAGE(CXX)

FIND_PACKAGE(xbmc REQUIRED)
FIND_PACKAGE(xbmcplatform REQUIRED)
FIND_PACKAGE(TinyXML REQUIRED)

addon_version(pvr.mediaportal.tvserver MPTV)

INCLUDE_DIRECTORIES(${xbmcplatform_INCLUDE_DIRS}
                    ${TINYXML_INCLUDE_DIR}
                    ${XBMC_INCLUDE_DIR}
                    ${PROJECT_SOURCE_DIR}/src)
ADD_DEFINITIONS(-D__STDC_FORMAT_MACROS)
IF (NOT WIN32)
  include(AddOptions.cmake)
  add_options(ALL_LANGUAGES ALL_BUILDS "-fPIC")
ENDIF(NOT WIN32)

SET(SOURCES src/Cards.cpp
            src/channels.cpp
            src/client.cpp
            src/epg.cpp
            src/GenreTable.cpp
            src/pvrclient-mediaportal.cpp
            src/recordings.cpp
            src/Socket.cpp
            src/timers.cpp
            src/uri.cpp
            src/utils.cpp)

ADD_SUBDIRECTORY(src/lib/tsreader)

SET(DEPLIBS ${xbmcplatform_LIBRARIES}
            ${TINYXML_LIBRARIES} tsreader)

build_addon(pvr.mediaportal.tvserver SOURCES DEPLIBS MPTV_VERSION)
install_addon(pvr.mediaportal.tvserver ${MPTV_VERSION})
