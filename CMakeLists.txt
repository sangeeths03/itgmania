# Install the ITGmania app bundle to the install prefix
install(TARGETS ITGmania
        BUNDLE
        DESTINATION .)

cmake_minimum_required(VERSION 3.20)

project(StepMania)

include(StepmaniaCore.cmake)

# The external libraries need to be included.
add_subdirectory(extern)

# The internal libraries and eventual executable to be used.
add_subdirectory(src)
