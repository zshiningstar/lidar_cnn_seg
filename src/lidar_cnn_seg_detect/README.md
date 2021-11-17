# CNN LiDAR Baidu Object Segmenter

rockauto package based on Baidu's object segmenter.

## The Pretrained model
Use this link to download the pretrained model from Baidu:

https://github.com/ApolloAuto/apollo/tree/master/modules/perception/production/data/perception/lidar/models/cnnseg

These two files are needed:
* deploy.prototxt
* deploy.caffemodel

## How to launch

* From a sourced terminal:

`rosrun lidar_cnn_seg_detect lidar_cnn_seg_detect _network_definition_file:=/PATH/TO/FILE.prototxt _pretrained_model_file:=/PATH/TO/WEIGHTS.caffemodel _points_src:=/points_raw`

`roslaunch lidar_cnn_seg_detect lidar_cnn_seg_detect.launch network_definition_file:=/PATH/TO/FILE.prototxt pretrained_model_file:=/PATH/TO/WEIGHTS.caffemodel points_src:=/points_raw`

* From Runtime Manager:

Computing Tab -> Detection/ lidar_detector -> `cnn_segmenter_baidu`

## Parameters

|Parameter| Type| Description|Default|
----------|-----|--------|----|
|`network_definition_file`|*String*|Path to the network definition file (prototxt)||
|`pretrained_model_file`|*String* |Path to the Pretrained model (weights)||
|`points_src`|*String*|Input topic Pointcloud. Default.|`/points_raw`|
|`score_threshold`|*Double*|Minimum score required as given by the network to include the result (0.-1.)|0.6|
|`use_gpu`|*Bool*|Whether ot not to use a GPU device|`true`|
|`gpu_device_id`|*Int*|GPU ID|`0`|

## Outputs

|Topic|Type|Description|
|---|---|---|
|`/detection/lidar_detector/points_cluster`|`sensor_msgs/PointCloud2`|Colored PointCloud of the resulting detected objects|
|`/detection/lidar_detector/objects`|`rockauto_msgs/DetectedObjetArray`|Array of Detected Objects in rockauto format|

## Notes

To display the results in Rviz `objects_visualizer` is required.
(Launch file launches automatically this node).