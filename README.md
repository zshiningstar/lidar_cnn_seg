## 深度学习Lidar障碍物检测分类
* 参考:https://github.com/AbangLZU/cnn_seg_lidar

![results](https://github.com/zshiningstar/lidar_cnn_seg/blob/cnn_seg_caffe/results/results.png)

**以下环境安装必须按照本文档书写顺序,否则报错**
### 运行环境(首先必须保证自己电脑带有独立显卡)
* Ubuntu 16.04
* ROS kinetic
* CUDA 10.0
* Caffe

### 一 环境配置

#### 1 安装caffe
* 安装依赖

```sh
sudo apt-get install libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libopenblas-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
```

* 下载caffe
```
git clone https://github.com/zshiningstar/caffe.git
```

* 将本项目下的Makefile.config替换在caffe下的对应文件
* 安装编译caffe
```
sudo make -j8
sudo make distribute
```
#### 2 安装NVIDIA
参见本路径下env.md

### 二 编译此项目
进入雷达深度学习检测功能包所在工作空间下
```
catkin_make
```

### 三 启动
```
source devel/setup.bash
roslaunch lidar_cnn_seg_detect lidar_cnn_seg_detect.launch 
```
### 四 遇到问题
参考:https://blog.csdn.net/qq_40660130/article/details/121382805

