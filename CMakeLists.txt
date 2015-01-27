# CMake Version
cmake_minimum_required(VERSION 2.8)

# Project Name
project(SQLite)

# Output Dir
#set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/../../../../Build/Lib)

# Set Source/Headers
set(Lib_Headers ${PROJECT_SOURCE_DIR}/sqlite3.h)
set(Lib_Source ${PROJECT_SOURCE_DIR}/sqlite3.c)

# Add Source/Headers
list(APPEND Lib_Headers ${PROJECT_SOURCE_DIR}/sqlite3ext.h)

# Link dirs
link_directories(${PROJECT_SOURCE_DIR})
include_directories(${PROJECT_SOURCE_DIR})

# Library Build
add_library(SQLite SHARED ${Lib_Source} ${Lib_Headers})
set_target_properties(SQLite PROPERTIES LINKER_LANGUAGE C)
set_target_properties(SQLite PROPERTIES OUTPUT_NAME "SQLite")

# Linker
if (WIN32)
    target_link_libraries(SQLite winmm gdi32 c++abi)
elseif (APPLE)
    target_link_libraries(SQLite "-framework Foundation -framework IOKit -framework Carbon -framework CoreFoundation" c++abi)
elseif (UNIX)
    target_link_libraries(SQLite c++abi)
endif()

