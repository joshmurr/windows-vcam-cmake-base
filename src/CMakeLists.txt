cmake_minimum_required(VERSION 3.5)
project(virtual-cam)

set(virtualcam_HEADERS
	virtual-cam.h
	)

set(virtualcam_SOURCES
  dllmain.cpp
  virtual-cam.cpp
  virtual-cam.def
  )

if(CMAKE_SIZEOF_VOID_P EQUAL 8)
  # This is true
  find_library(DShowLib strmbase PATHS "${DShow}/x64" NO_DEFAULT_PATH)
  find_library(DShowLibD strmbasd PATHS "${DShow}/x64" NO_DEFAULT_PATH)
else()
  find_library(DShowLib strmbase PATHS "${DShow}/x86" NO_DEFAULT_PATH)
  find_library(DShowLibD strmbasd PATHS "${DShow}/x86" NO_DEFAULT_PATH)
endif()

add_library(virtual-cam MODULE
  ${virtualcam_HEADERS}
  ${virtualcam_SOURCES}
)

include_directories(
  ${Baseclasses}
  )

SET(DSHOW_LIBRARY optimized ${DShowLib} debug ${DShowLibD})	

target_link_libraries(virtual-cam
  ${DSHOW_LIBRARY}
  winmm
  Strmiids
  )

if(MSVC)
  set(CMAKE_EXE_LINKER_FLAGS
    "${CMAKE_EXE_LINKER_FLAGS} /DEF:virtual-cam.def /NODEFAULTLIB")

  foreach(var CMAKE_CXX_FLAGS CMAKE_CXX_FLAGS_DEBUG CMAKE_CXX_FLAGS_RELEASE
      CMAKE_CXX_FLAGS_MINSIZEREL CMAKE_CXX_FLAGS_RELWITHDEBINFO)
    if(${var} MATCHES "/MD")
      string(REGEX REPLACE "/MD" "/MT" ${var} "${${var}}")
    endif()
  endforeach()	

endif()
SET(CMAKE_MODULE_LINKER_FLAGS_DEBUG "${CMAKE_MODULE_LINKER_FLAGS_DEBUG} /SAFESEH:NO")
SET(CMAKE_MODULE_LINKER_FLAGS_RELEASE "${CMAKE_MODULE_LINKER_FLAGS_RELEASE} /SAFESEH:NO")

include(CopyMSVCBins)
