cmake_minimum_required(VERSION 2.4.6)
include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

rosbuild_init()

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

include(FindPkgConfig)
pkg_check_modules(OPENNI libopenni)

include(FindGLUT)
include_directories(${GLUT_INCLUDE_DIR})

include_directories(${OPENNI_INCLUDEDIR} /usr/include/ni)

include_directories(${PROJECT_SOURCE_DIR})

rosbuild_add_executable(user_selection src/main.cpp 
										src/ClosestUserSelector.cpp
										src/DefaultTrackingInitializer.cpp
										src/ExitPoseDetector.cpp
										src/opengles.cpp
										src/PoseToggleUserSelector.cpp
										src/PoseUserSelector.cpp
										src/SampleManager.cpp
										src/SceneDrawer.cpp
										src/SinglePoseUserSelector.cpp
										src/TrackingInitializer.cpp
										src/UserSelector.cpp
										src/UserTracker.cpp)

target_link_libraries(user_selection ${OPENNI_LIBRARIES} ${GLUT_LIBRARIES})
