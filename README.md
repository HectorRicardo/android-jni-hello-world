# android-jni-hello-world

This repo shows a minimal reproducible example of how to integrate Android Java code with native C++
code.

The following are notes that I took while reading through the official Android documentation.

## General Overview: how to add C/C++ code to your Android project?

1. Place the C/C++ code in a `cpp` directory inside [`/src/app/main`](app/src/main).
2. Create a `CMakeLists.txt` build script in the `cpp` directory. See the comments in
   [`CMakeLists.txt`](app/src/main/cpp/CMakeLists.txt).
3. In the module's `build.gradle` file, provide the path to `CMakeLists.txt`, along with optional
   parameters. See the comments in [`app/build.gradle`](app/build.gradle).
4. Java or Kotlin code can then call functions in your native library through JNI.

## What happens when you build a project with C/C++?

1. Gradle calls upon your external build script, `CMakeLists.txt`.
2. Cmake follows the commands in the `CMakeLists.txt` build script to compile the C/C++ code into a
   *native library*, which is a shared object library (a `.so` file).
    - If a native library is named `native-lib`, the resulting `.so` file is called
      `libnative-lib.so`.
    - It prepends "`lib`" and uses the `.so` extension. See the comments in
      [`CMakeLists.txt`](app/src/main/cpp/CMakeLists.txt).
3. Gradle packages this `.so` file in your app’s APK.

## What happens when you run a project with C/C++?

1. Java/Kotlin code loads the native library using `System.loadLibrary(libraryName)`.
    - Pass the library name as a string. For example, `System.loadLibrary("native-lib")`.
2. Java/Kotlin can call any native function as a normal Java/Kotlin function. See JNI rules.
