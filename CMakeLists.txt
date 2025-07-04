cmake_minimum_required(VERSION 3.20)

project(StepMania VERSION 1.1.0)

include(StepmaniaCore.cmake)

# The external libraries need to be included.
add_subdirectory(extern)

# The internal libraries and eventual executable to be used.
add_subdirectory(src)

# --- CPACK CONFIG ---
# Generate a unique volume name using timestamp and commit hash
execute_process(
  COMMAND git rev-parse --short HEAD
  WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
  OUTPUT_VARIABLE GIT_COMMIT_HASH
  OUTPUT_STRIP_TRAILING_WHITESPACE
)

# Fallback hash if git is not available
if(NOT GIT_COMMIT_HASH)
  set(GIT_COMMIT_HASH "unknown")
endif()

string(TIMESTAMP TS "%Y%m%d-%H%M%S")

set(CPACK_GENERATOR "DragNDrop")
set(CPACK_DMG_VOLUME_NAME "ITGmania-${CMAKE_SYSTEM_PROCESSOR}-${TS}-${GIT_COMMIT_HASH}")
set(CPACK_PACKAGE_FILE_NAME "ITGmania-${CMAKE_SYSTEM_PROCESSOR}-${TS}-${GIT_COMMIT_HASH}")
set(CPACK_PACKAGE_VERSION ${PROJECT_VERSION})

include(CPack)
