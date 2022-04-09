# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build native libraries.
# This ensures that a certain set of CMake features is available to the build.

cmake_minimum_required(VERSION 3.18.1)

# Declares and names the project.

project("cplusplusscratch")

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries by adding multiple
# add_library() commands, and CMake builds them for you.
# When you build your app, Gradle automatically packages shared
# libraries with your APK (Note: ONLY shared libraries).

# You can define multiple `add_library()` commands,
# each of which will define a single native library.
# For every `add_library()` command you add,
# you load its associated library in Java/Kotlin with `System.loadLibrary()`.

add_library(
        # Sets the name of the library.
        # This is the string you will pass to `System.loadLibrary()`.
        cplusplusscratch

        # Sets the library as a shared library.
        SHARED

        # Provides the path to your source file(s),
        # relative to the directory in which `CMakeList.txt` lives.
        # Best practice: put `CMakeList.txt` in `src/app/main/cpp`.
        # Space-separated source code file paths.
        native-lib.cpp)

# Searches for a specified prebuilt library and stores its path as a
# variable. Because CMake includes system libraries in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library(
        # Defines the name of the path variable
        # that stores the location of the NDK library.
        # You use this variable to refer to the NDK library
        # in other parts of the build script.
        log-lib

        # Specifies the name of the NDK library that CMake should locate.
        log)

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries(
        # Specifies the target library.
        cplusplusscratch

        # Links the log library included in the NDK to the target library.
        # Space-separated list of path variables
        # (defined in the `find_library()` commands above)
        ${log-lib})
