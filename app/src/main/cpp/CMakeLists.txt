# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
        native-lib

        # Sets the library as a shared library.
        SHARED

        # Provides a relative path to your source file(s).
        ffmpegs/cmdutils.c
        ffmpegs/ffmpeg.c
        ffmpegs/ffmpeg_filter.c
        ffmpegs/ffmpeg_opt.c
        ffmpegs/ffmpeg_hw.c
        native-lib.cpp)


add_library( ffmpeg #切记不要用libffmpeg
        SHARED
        IMPORTED )
set_target_properties( ffmpeg
        PROPERTIES IMPORTED_LOCATION
        ../../../../libs/${ANDROID_ABI}/libffmpeg.so)



find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)

include_directories(ffmpegs)

target_link_libraries( # Specifies the target library.
        native-lib
        ffmpeg

        # Links the target library to the log library
        # included in the NDK.
        ${log-lib})