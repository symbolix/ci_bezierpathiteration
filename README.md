# ci_BezierPathIteration #

## Intro ##

This is an example libcinder project that should demonstrate app build process
outside the cinder project structure.

## Commands ##

1. From within the `./build` folder, run the following command: `cmake .. -DCINDER_VERBOSE=On -DCMAKE_BUILD_TYPE=Release`

2. After the build process is complete, run `make` to compile the application. Once the application is successfully compiled the `BezierPathIteration.app` folder will be created inside the following location: `./build/<build_type>/BezierPathIteration.app`

3. To run the application, just run `open BezierPathIteration.app`