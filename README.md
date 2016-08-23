# ci_BezierPathIteration #

## Intro ##

This is an example libcinder project that should demonstrate app build process
outside the cinder project structure.

## Commands ##

1. From within the `./build` folder, run the following command: `cmake .. -DCINDER_VERBOSE=On -DCMAKE_BUILD_TYPE=Release`

2. After the build process is complete, run `make` to compile the application. Once the application is successfully compiled the `BezierPathIteration.app` folder will be created inside the following location: `./build/<build_type>/BezierPathIteration.app`

3. To run the application, just run `open BezierPathIteration.app`

## How this works? ##

* The first item that is critical to this process is the `CINDER_PATH` variable.
This should be pointing to the `libcinder` folder structure.

* The initial `CMakeLists.txt` file is providing some basic information
  regarding the project.

* The required CMake module `cinderMakeApp` is located inside the `./cmake`
  folder. Once the local `./cmake` folder is appended to the `${CMAKE_MODULE_PATH}`, the `cinderMakeApp.cmake` file is included and the `ci_make_app` function becomes available.

* The `ci_make_app` function is a wrapper that accepts various arguments and
  the intention is to fecth the configuration from the CMake chain located inside
  the `CINDER_PATH` structure.

* The first script accessed from the remote `CINDER_PATH` location is `${CINDER_PATH}/proj/cmake/configure.cmake'

* After that `libcinder` is imported from the following location as na
  `imported target`:
  `${CINDER_PATH}/lib/<platform>/<build_type>` which in the current case under `OSX`, would be `${CINDER_PATH}/lib/macosx/Release`. There should be a `cinderConfig.cmake` file ready in that location beside the static lib archive `libcinder.a` (yes, we have `libcinder` built as a STATIC target). The file is created as part of the build process that compiles the `libcinder` target.

* The `cinderConfig.cmake` inside `${CINDER_PATH}/lib/macosx/Release`will be invoking a `cinderTargets.cmake` file that has been created as part of the build process that compiled `libcinder`. The `cinderTargets.cmake` file should be located inside the `build` folder of `libcinder`, in that case it is `${CINDER_PATH}/build/lib/macosx/Release//cinderTargets.cmake`.

* At the final stage, `icons` and `assets` are copied to the `Resources`
  folder.
