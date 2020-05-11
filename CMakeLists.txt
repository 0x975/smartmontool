cmake_minimum_required (VERSION 3.13.0)

project (smartmontools)

set(_HDR
  atacmdnames.h
  atacmds.h
  csmisas.h
  dev_areca.h
  dev_ata_cmd_set.h
  dev_interface.h
  dev_tunnelled.h
  drivedb.h
  getopt/getopt.h
  knowndrives.h
  regex/regex.h
  regex/regex_internal.h
  scsicmds.h
  utility.h

  aacraid.h
  ataidentify.h
  ataprint.h
  dev_intelliprop.h
  json.h
  nvmecmds.h
  nvmeprint.h
  scsiprint.h
  smartctl.h
  static_assert.h
  
  getopt/getopt_int.h
  getopt/bits/getopt_ext.h
  getopt/bits/getopt_core.h
)

set(_SRC
  atacmdnames.cpp
  atacmds.cpp
  dev_areca.cpp
  dev_ata_cmd_set.cpp
  dev_interface.cpp
  getopt/getopt.c
  getopt/getopt1.c
  knowndrives.cpp
  regex/regex.c
  scsiata.cpp
  scsicmds.cpp
  scsinvme.cpp
  utility.cpp

  ataidentify.cpp
  ataprint.cpp
  dev_intelliprop.cpp
  dev_jmb39x_raid.cpp
  json.cpp
  nvmecmds.cpp
  nvmeprint.cpp
  scsiprint.cpp
  smartctl.cpp
)

set(WIN_
  os_win32/wmiquery.h
  os_win32/config.h
  os_win32/svnversion.h
  os_win32/wmiquery.cpp
  os_win32/popen.h
  os_win32.cpp
)

set(UNIX_
  unix/config.h
  unix/svnversion.h
  os_linux.h
  os_linux.cpp
)

if(MSVC)
  set(ALL_FILES ${_HDR} ${_SRC} ${WIN_})

  add_compile_definitions(_GETOPT_STANDALONE)
  add_compile_definitions(_REGEX_STANDALONE)

  include_directories("${CMAKE_SOURCE_DIR}/os_win32")
endif()

if (UNIX)
  set(ALL_FILES ${_HDR} ${_SRC} ${UNIX_})

  add_compile_definitions(_GETOPT_STANDALONE)
  add_compile_definitions(_REGEX_STANDALONE)
  add_compile_definitions(SMARTMONTOOLS_SYSCONFDIR=\"/usr/local/etc\")

  include_directories("${CMAKE_SOURCE_DIR}/unix")
endif ()

include_directories("${CMAKE_SOURCE_DIR}")
include_directories("${CMAKE_SOURCE_DIR}/regex")
include_directories("${CMAKE_SOURCE_DIR}/getopt")

# use config.h
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DHAVE_CONFIG_H")

add_library(${PROJECT_NAME} STATIC ${ALL_FILES})
