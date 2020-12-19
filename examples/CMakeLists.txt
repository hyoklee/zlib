cmake_minimum_required (VERSION 3.10)
PROJECT (ZLIB_EXAMPLES)

#-----------------------------------------------------------------------------
# Add Tests
#-----------------------------------------------------------------------------

#-- Adding test for enough
add_executable (enough enough.c)
target_include_directories(enough PRIVATE "${ZLIB_SOURCE_DIR}")
TARGET_C_PROPERTIES (enough STATIC)
target_link_libraries (enough PRIVATE ${ZLIB_LIB_TARGET})

add_test (NAME enough COMMAND $<TARGET_FILE:enough>)

#-- Adding test for fitblk
add_executable (fitblk fitblk.c)
target_include_directories(fitblk PRIVATE "${ZLIB_SOURCE_DIR}")
TARGET_C_PROPERTIES (fitblk STATIC)
target_link_libraries (fitblk PRIVATE ${ZLIB_LIB_TARGET})

#add_test (NAME fitblk COMMAND $<TARGET_FILE:fitblk> #)

#-- Adding test for gun
#if (NOT WIN32)
#  add_executable (gun gun.c)
#  target_include_directories(gun PRIVATE "${ZLIB_SOURCE_DIR}")
#  TARGET_C_PROPERTIES (gun STATIC)
#  target_link_libraries (gun PRIVATE ${ZLIB_LIB_TARGET})
#endif (NOT WIN32)

#add_test (NAME gun COMMAND $<TARGET_FILE:gun> file1 file2)

#-- Adding test for gzappend
add_executable (gzappend gzappend.c)
target_include_directories(gzappend PRIVATE "${ZLIB_SOURCE_DIR}")
TARGET_C_PROPERTIES (gzappend STATIC)
target_link_libraries (gzappend PRIVATE ${ZLIB_LIB_TARGET})

add_test (NAME gzappend COMMAND $<TARGET_FILE:gzappend>)

#-- Adding test for gzjoin
add_executable (gzjoin gzjoin.c)
target_include_directories(gzjoin PRIVATE "${ZLIB_SOURCE_DIR}")
TARGET_C_PROPERTIES (gzjoin STATIC)
target_link_libraries (gzjoin PRIVATE ${ZLIB_LIB_TARGET})

add_test (NAME gzjoin COMMAND $<TARGET_FILE:gzjoin>)

#-- Adding test for gzlog
#add_executable (gzlog gzlog.c)
#target_include_directories(gzlog PRIVATE "${ZLIB_SOURCE_DIR}")
#TARGET_C_PROPERTIES (gzlog STATIC)
#target_link_libraries (gzlog PRIVATE ${ZLIB_LIB_TARGET})
#
#add_test (NAME gzlog COMMAND $<TARGET_FILE:gzlog>)

#-- Adding test for zpipe
add_executable (zpipe zpipe.c)
target_include_directories(zpipe PRIVATE "${ZLIB_SOURCE_DIR}")
TARGET_C_PROPERTIES (zpipe STATIC)
target_link_libraries (zpipe PRIVATE ${ZLIB_LIB_TARGET})

#add_test (NAME zpipe COMMAND $<TARGET_FILE:zpipe> file1 file2)

#-- Adding test for zran
add_executable (zran zran.c)
target_include_directories(zran PRIVATE "${ZLIB_SOURCE_DIR}")
TARGET_C_PROPERTIES (zran STATIC)
target_link_libraries (zran PRIVATE ${ZLIB_LIB_TARGET})

#add_test (NAME zran COMMAND $<TARGET_FILE:zran> file)

######################################################
#  examples for 64 bits
######################################################
if (HAVE_OFF64_T)
  #-- Adding test for enough64
  add_executable (enough64 enough.c)
  target_include_directories(enough64 PRIVATE "${ZLIB_SOURCE_DIR}")
  TARGET_C_PROPERTIES (enough64 STATIC)
  target_compile_options(enough64 PRIVATE
      $<$<C_COMPILER_ID:MSVC>:-D_FILE_OFFSET_BITS=64>
      $<$<CXX_COMPILER_ID:MSVC>:-D_FILE_OFFSET_BITS=64>
  )
  target_link_libraries (enough64 PRIVATE ${ZLIB_LIB_TARGET})

  add_test (NAME enough64 COMMAND $<TARGET_FILE:enough64>)

  #-- Adding test for fitblk64
  add_executable (fitblk64 fitblk.c)
  target_include_directories(fitblk64 PRIVATE "${ZLIB_SOURCE_DIR}")
  TARGET_C_PROPERTIES (fitblk64 STATIC)
  target_compile_options(fitblk64 PRIVATE
      $<$<C_COMPILER_ID:MSVC>:-D_FILE_OFFSET_BITS=64>
      $<$<CXX_COMPILER_ID:MSVC>:-D_FILE_OFFSET_BITS=64>
  )
  target_link_libraries (fitblk64 PRIVATE ${ZLIB_LIB_TARGET})

#  add_test (NAME fitblk64 COMMAND $<TARGET_FILE:fitblk64> #)
endif (HAVE_OFF64_T)
