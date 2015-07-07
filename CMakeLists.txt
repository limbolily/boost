cmake_minimum_required(VERSION 2.8)

include("yong_injector/injector.cmake")

yong_project(boost CXX)

file(GLOB BOOST_LIBS "${CMAKE_CURRENT_SOURCE_DIR}/libs/*")

foreach(boost_lib ${BOOST_LIBS})
  if (EXISTS "${boost_lib}/include")
    yong_install_header_directories(boost
      DIRECTORIES "${boost_lib}/include/boost"
      FILES_MATCHING
        PATTERN "*.hpp" PATTERN "*.ipp" PATTERN "*.h"
        PATTERN "*.inc" PATTERN "*.SUNWCCh"
        PATTERN "CVS" EXCLUDE PATTERN ".svn" EXCLUDE
        )
    include_directories("${boost_lib}/include")
  endif()
endforeach()

file(GLOB BOOST_NUMERIC_HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/libs/numeric/*")
foreach(boost_numeric_header ${BOOST_NUMERIC_HEADERS})
  if (EXISTS "${boost_numeric_header}/include/boost")
    yong_install_header_directories(boost
      DIRECTORIES "${boost_numeric_header}/include/boost"
      FILES_MATCHING
        PATTERN "*.hpp" PATTERN "*.ipp" PATTERN "*.h"
        PATTERN "*.inc" PATTERN "*.SUNWCCh"
        PATTERN "CVS" EXCLUDE PATTERN ".svn" EXCLUDE
        )
    include_directories("${boost_numeric_header}/include")
  endif()
endforeach()

yong_install_header_directories(boost
  DIRECTORIES "${CMAKE_CURRENT_SOURCE_DIR}/libs/compatibility/include/boost"
  FILES_MATCHING
    PATTERN "*"
    PATTERN "*.hpp" EXCLUDE
    PATTERN "*.h" EXCLUDE
    PATTERN "*.ipp" EXCLUDE
    PATTERN "*.inc" EXCLUDE
    PATTERN "*.SUNWCCh" EXCLUDE
    PATTERN "CVS" EXCLUDE
    PATTERN ".svn" EXCLUDE
    )

yong_install_header_directories(boost
  DIRECTORIES "${CMAKE_CURRENT_SOURCE_DIR}/libs/tr1/include/boost"
  FILES_MATCHING
    PATTERN "*"
    PATTERN "*.hpp" EXCLUDE
    PATTERN "*.h" EXCLUDE
    PATTERN "*.ipp" EXCLUDE
    PATTERN "*.inc" EXCLUDE
    PATTERN "*.SUNWCCh" EXCLUDE
    PATTERN "CVS" EXCLUDE
    PATTERN ".svn" EXCLUDE
    )

add_definitions(-DBOOST_ALL_NO_LIB=1)

add_subdirectory("libs/system")
add_subdirectory("libs/filesystem")
add_subdirectory("libs/regex")
add_subdirectory("libs/graph")
add_subdirectory("libs/iostreams")
#add_subdirectory("libs/locale")
add_subdirectory("libs/chrono")
add_subdirectory("libs/thread")
add_subdirectory("libs/serialization")

yong_project_end()
