cmake_minimum_required(VERSION 3.20)

project(StepMania VERSION 0.1.0)

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

# 🔹 Set app bundle properties
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

# ✅ Also install essential runtime folders into the .app bundle
# Adjust folder names if needed
install(DIRECTORY
    ${CMAKE_SOURCE_DIR}/Themes
    ${CMAKE_SOURCE_DIR}/Scripts
    ${CMAKE_SOURCE_DIR}/Announcers
    ${CMAKE_SOURCE_DIR}/BackgroundEffects
    ${CMAKE_SOURCE_DIR}/NoteSkins
    ${CMAKE_SOURCE_DIR}/Characters
    ${CMAKE_SOURCE_DIR}/Courses
    ${CMAKE_SOURCE_DIR}/Data
    ${CMAKE_SOURCE_DIR}/Metrics
    ${CMAKE_SOURCE_DIR}/BGAnimations
    DESTINATION ITGmania.app/Contents/Resources
)
