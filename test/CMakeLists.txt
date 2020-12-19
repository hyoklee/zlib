cmake_minimum_required (VERSION 3.10)
PROJECT (ZLIB_TEST)

#-----------------------------------------------------------------------------
# Add Tests
#-----------------------------------------------------------------------------

#-- Adding test for example
add_executable (example example.c)
target_include_directories(example PRIVATE "${ZLIB_SOURCE_DIR}")
TARGET_C_PROPERTIES (example STATIC)
target_link_libraries (example PRIVATE ${ZLIB_LIB_TARGET})

add_test (NAME example COMMAND $<TARGET_FILE:example>)

#-- Adding test for infcover
#add_executable (infcover infcover.c)
#target_include_directories(example PRIVATE "${ZLIB_SOURCE_DIR}")
#TARGET_C_PROPERTIES (infcover STATIC)
#target_link_libraries (infcover PRIVATE ${ZLIB_LIB_TARGET})
#
#add_test (NAME infcover COMMAND $<TARGET_FILE:infcover>)

#-- Adding test for minigzip
add_executable (minigzip ../minigzip.c)
target_include_directories(minigzip PRIVATE "${ZLIB_SOURCE_DIR}")
TARGET_C_PROPERTIES (minigzip STATIC)
target_link_libraries (minigzip PRIVATE ${ZLIB_LIB_TARGET})

#add_test (NAME minigzip COMMAND $<TARGET_FILE:minigzip>)


if (HAVE_OFF64_T)
  #-- Adding test for example64
  add_executable (example64 ../example.c)
  target_include_directories(example64 PRIVATE "${ZLIB_SOURCE_DIR}")
  TARGET_C_PROPERTIES (example64 STATIC)
  target_compile_options(example64 PRIVATE
      $<$<C_COMPILER_ID:MSVC>:-D_FILE_OFFSET_BITS=64>
      $<$<CXX_COMPILER_ID:MSVC>:-D_FILE_OFFSET_BITS=64>
  )
  target_link_libraries (example64 PRIVATE ${ZLIB_LIB_TARGET})

  add_test (NAME example64 COMMAND $<TARGET_FILE:example64>)

  #-- Adding test for minigzip64
  add_executable (minigzip64 ../minigzip.c)
  target_include_directories(minigzip64 PRIVATE "${ZLIB_SOURCE_DIR}")
  TARGET_C_PROPERTIES (minigzip64 STATIC)
  target_compile_options(minigzip64 PRIVATE
      $<$<C_COMPILER_ID:MSVC>:-D_FILE_OFFSET_BITS=64>
      $<$<CXX_COMPILER_ID:MSVC>:-D_FILE_OFFSET_BITS=64>
  )
  target_link_libraries (minigzip64 PRIVATE ${ZLIB_LIB_TARGET})

#  add_test (NAME minigzip64 COMMAND $<TARGET_FILE:minigzip64>)
endif (HAVE_OFF64_T)
