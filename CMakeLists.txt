cmake_minimum_required(VERSION 3.20)

project(StepMania)

# Load project-specific config if needed
include(StepmaniaCore.cmake)

# External dependencies
add_subdirectory(extern)

# 🔹 Collect all source files (adjust this to match your structure)
file(GLOB_RECURSE GAME_SOURCES
    src/*.cpp
    src/*.c
    src/*.h
)

# 🔹 Create the macOS .app bundle
add_executable(ITGmania MACOSX_BUNDLE
    ${GAME_SOURCES}
)

# 🔹 Link external libraries (adjust to your project’s needs)
target_link_libraries(ITGmania
    PRIVATE
    SDL2
    # Add other required libraries here
)

# 🔹 Optional: Set app bundle properties (Info.plist, icon, etc.)
set_target_properties(ITGmania PROPERTIES
    MACOSX_BUNDLE_BUNDLE_NAME "ITGmania"
    MACOSX_BUNDLE_GUI_IDENTIFIER "com.itgmania"
    MACOSX_BUNDLE_BUNDLE_VERSION "${PROJECT_VERSION}"
    MACOSX_BUNDLE_SHORT_VERSION_STRING "${PROJECT_VERSION}"
    # MACOSX_BUNDLE_INFO_PLIST "${CMAKE_SOURCE_DIR}/Info.plist"  # Optional
)

# ✅ Install .app to prefix (used by GitHub Actions DMG step)
install(TARGETS ITGmania
    BUNDLE
    DESTINATION .
)
