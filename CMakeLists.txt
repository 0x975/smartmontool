cmake_minimum_required (VERSION 3.13.0)

project (smartmontools)

set(_HDR
  atacmdnames.h
  atacmds.h
  config.h
  csmisas.h
  dev_areca.h
  dev_ata_cmd_set.h
  dev_interface.h
  dev_tunnelled.h
  drivedb.h
  getopt/getopt.h
  int64.h
  knowndrives.h
  os_win32/wbemcli_small.h
  os_win32/wmiquery.h
  regex/regex.h
  regex/regex_internal.h
  scsicmds.h
  svnversion.h
  utility.h
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
  os_win32.cpp
  os_win32/wmiquery.cpp
  regex/regex.c
  scsiata.cpp
  scsicmds.cpp
  utility.cpp
)

include_directories("${CMAKE_SOURCE_DIR}")
include_directories("${CMAKE_SOURCE_DIR}/regex")

# use config.h
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DHAVE_CONFIG_H")

add_library(${PROJECT_NAME} STATIC ${_HDR} ${_SRC})
