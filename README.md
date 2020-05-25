# Welcome

This is a work in progress started on May 2020.  Original openvslam is being adapted to be built on eclipse instead of using cmake, to allow programmers modify the code mainly for testing and usability purposes.

This project is built in eclipse CDT with C++17 and opencv 4, on Ubuntu 20.04.  Should work on any:

- C++11+ (this can change if I start rewritting using ranges)
- any C++ IDE, but tips in this file asume you're using eclipse CDT and gcc
- opencv 3+
- any Debian (it includes any Ubuntu, any Linux Mint...)

This readme will be updated with status and compilation tips.  Please read `ORIGINAL README.md`, a copy from the original openvslam README.


# Status

May 25, 2020, it compiles and runs, interactive GUI appears on screen, two threads have names (openVSLAM and Viewer, useful for debugging), but it isn't grabing images from input video file.  No errors.

# Compilation tips

You need dependencies installed as indicated in openvslam installation manual.

You also need orb_vocab_dbow2, a 44MB file provided with openvslam.

The following setting are already set up in eclipse `.project` files in this repository.

## Libraries settings

You'll need to set up these dependencies libraries in your IDE:

Assuming local viewer (I didn't try web viewer):
- pangolin
- GL
- GLEW

OpenCV (this list may contain some unneeded opencv library):
- opencv_core
- opencv_imgproc
- opencv_highgui
- opencv_features2d
- opencv_calib3d
- opencv_video
- opencv_videio
- opencv_imgcodecs

g2o:
- g2o_core
- g2o_stuff
- g2o_types_sba
- g2o_types_sim3
- g2o_solver_dense
- g2o_solver_eigen
- g2o_solver_csparse
- g2o_csparse_extension
- cxsparse

other:
- gomp
- tbb
- yaml-cpp


## Include paths

- /usr/include/suitesparse
- /usr/local/include/eigen3
- /usr/local/include/opencv4    <= Only if you have opencv 4!
- "${workspace_loc:/${ProjName}/src}"
- "${workspace_loc:/${ProjName}/3rd/popl/include}"
- "${workspace_loc:/${ProjName}/3rd/spdlog/include}"
- "${workspace_loc:/${ProjName}/3rd/json/include}"

## Preprocessor constants

Also, set up these preprocessor settings in your IDE:

- USE_PANGOLIN_VIEWER
- USE_DBOW2

## Miscelanous

- GCC C++ compiler dialect: ISO C++17
- GCC C++ compiler miscelanous: Support for pthreads
- GCC Linker General: Support for pthreads

May there be warnings about uninitialized members en spdlog/thread_pool.h .

## Exclude source

This folders are excluded from compilation:

- cmake
- docs
- example
- ros
- test
- src/socket_publisher

# Changes in code

- Some zero initialization on uninitialized members to silence warnings
- Changed #include <Eigen/... with #include <eigen3/Eigen/... because eigen3/Eigen can be found in usual include path.  Adding the include path /usr/local/include/eigen3 didn't work for me, I don't know why.
- src/main.cc is based on example/run_video_slam.cc
