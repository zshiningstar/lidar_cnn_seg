cmake_minimum_required(VERSION 2.8.3)
project(lidar_cnn_seg_detect)

find_package(catkin REQUIRED COMPONENTS
        rockauto_build_flags
        roscpp
        tf
        tf_conversions
        pcl_ros
        sensor_msgs
        geometry_msgs
        rockauto_msgs
        )

find_package(CUDA)
find_package(OpenCV REQUIRED)
# find_package(Caffe REQUIRED)

catkin_package(
        INCLUDE_DIRS
        include
        CATKIN_DEPENDS
        roscpp
        tf
        tf_conversions
        pcl_ros
        sensor_msgs
        geometry_msgs
        rockauto_msgs
)

IF (CUDA_FOUND)
    include_directories(${CUDA_INCLUDE_DIRS})

    IF ("${CMAKE_SYSTEM_PROCESSOR}" MATCHES "^arm")
        link_directories(/usr/lib/arm-linux-gnueabihf/tegra)
    endif ()
ENDIF ()

# if (Caffe_FOUND)
#         include_directories(
#                 include
#                 ${catkin_INCLUDE_DIRS}
#                 ${OpenCV_INCLUDE_DIRS}
#                 ${Caffe_INCLUDE_DIRS}
#         )

#         add_executable(lidar_cnn_seg_detect
#                 nodes/lidar_cnn_seg_detect_node.cpp
#                 nodes/cnn_segmentation.cpp
#                 nodes/cluster2d.cpp
#                 nodes/feature_generator.cpp
#                 )
#         target_link_libraries(lidar_cnn_seg_detect
#                 ${catkin_LIBRARIES}
#                 ${OpenCV_LIBRARIES}
#                 ${CUDA_LIBRARIES}
#                 ${CUDA_CUBLAS_LIBRARIES}
#                 ${CUDA_curand_LIBRARY}
#                 ${Caffe_LIBRARIES}
#                 glog
#                 )
#         add_dependencies(lidar_cnn_seg_detect
#                 ${catkin_EXPORTED_TARGETS}
#                 )

#         install(TARGETS
#                 lidar_cnn_seg_detect
#                 ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#                 LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#                 RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
#                 )
# else ()
#     message("'Caffe' is not installed. 'lidar_cnn_seg_detect' will not be built.")
# endif ()


###CAFFE
set(CAFFE_PATH "$ENV{HOME}/dependences/caffe/distribute")


if (EXISTS "${CAFFE_PATH}")

    include_directories(
            include
            ${catkin_INCLUDE_DIRS}
            ${OpenCV_INCLUDE_DIRS}
            ${CAFFE_PATH}/include
    )

    add_executable(lidar_cnn_seg_detect
            nodes/lidar_cnn_seg_detect_node.cpp
            nodes/cnn_segmentation.cpp
            nodes/cluster2d.cpp
            nodes/feature_generator.cpp
            )
    target_link_libraries(lidar_cnn_seg_detect
            ${catkin_LIBRARIES}
            ${OpenCV_LIBRARIES}
            ${CUDA_LIBRARIES}
            ${CUDA_CUBLAS_LIBRARIES}
            ${CUDA_curand_LIBRARY}
            ${CAFFE_PATH}/lib/libcaffe.so
            glog
            )
    add_dependencies(lidar_cnn_seg_detect
            ${catkin_EXPORTED_TARGETS}
            )

    install(TARGETS
            lidar_cnn_seg_detect
            ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
            LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
            RUNTIME DESTINATION ${CATKIN_GLOBAL_BIN_DESTINATION}
            )
else ()
    message("'Caffe' is not installed. 'lidar_cnn_seg_detect' will not be built.")
endif ()
