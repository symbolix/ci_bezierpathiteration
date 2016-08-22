# ci_BezierPathIteration #

## Intro ##

This is an example libcinder project that should demonstrate app build process
outside the cinder project structure.

## Commands ##

* From within the `./build` folder, run the following command:

```
cmake .. -DCINDER_VERBOSE=On -DCMAKE_BUILD_TYPE=Release
```

* Once the build process is complete, run the following command to compile the
  application:

  ```
  make
  ```

  This should compile the `BezierPathIteration.app` and place it inside the
  following folder:

  ```
  ./build/<build_type>/BezierPathIteration.app
  ```

  * To run the application, just run `open BezierPathIteration.app`
