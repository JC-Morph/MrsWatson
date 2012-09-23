file(GLOB vendor_FILES *.tar.gz)
foreach(vendor_file ${vendor_FILES})
  # This relies on semantic versioning for all third-party vendor tarballs
  string(REGEX MATCH "(.*).tar.gz" vendor_output_dir ${vendor_file})
  if(NOT IS_DIRECTORY ${CMAKE_MATCH_1})
    message(STATUS "Uncompressing ${vendor_file} -> ${CMAKE_MATCH_1}")
    execute_process(COMMAND tar xfz ${vendor_file} WORKING_DIRECTORY "vendor")
  endif()
endforeach()

# For windows, we can use a few common zip programs
#FIND_PROGRAM(ZIP_EXECUTABLE wzzip PATHS "$ENV{ProgramFiles}/WinZip")
#IF(ZIP_EXECUTABLE)
#SET(ZIP_COMMAND "\"${ZIP_EXECUTABLE}\" -P \"<ARCHIVE>\" @<FILELIST>")
#ENDIF(ZIP_EXECUTABLE)
#
#FIND_PROGRAM(ZIP_EXECUTABLE 7z PATHS "$ENV{ProgramFiles}/7-Zip") 
#IF(ZIP_EXECUTABLE)
#SET(ZIP_COMMAND "\"${ZIP_EXECUTABLE}\" a -tzip \"<ARCHIVE>\" @<FILELIST>")
#ENDIF(ZIP_EXECUTABLE)