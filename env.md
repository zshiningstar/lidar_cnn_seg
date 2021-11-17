### 1 安装NVIDIA驱动
> 下载驱动,对应自己显卡版本,在官网下载对应驱动,本电脑下载的为:NVIDIA-Linux-x86_64-440.100.run
https://www.nvidia.cn/geforce/drivers

#### 1.1 驱动安装
* 1.禁用nouveau,打开blacklist文件，在最后添加如下两行
```
sudo gedit /etc/modprobe.d/blacklist.conf

blacklist nouveau
options nouveau modeset=0
```
* 2.更新修改
```
sudo update-initramfs -u
```
* 3.电脑重启

* 4.验证nouveau已禁用,无输出则表示已禁用
```
lsmod | grep nouveau
```

* 5.ctrl+alt+f1进入命令行界面

* 6.关闭图形界面
```
sudo service lightdm stop
```
* 7.卸载系统中存在的驱动
```
sudo apt-get remove nvidia-*
```
* 8.安装驱动,弹出的提示窗口中均保持默认选择
```
sudo chmod  a+x NVIDIA-Linux-x86_64-440.100.run
sudo ./NVIDIA-Linux-x86_64-440.100.run -no-x-check -no-nouveau-check -no-opengl-files
```
* 9.重启图形界面
```
sudo service lightdm start
```
* 10.查看显卡
```
nvidia-smi
```
### 2 安装cuda 10.0
* 下载
https://developer.nvidia.com/cuda-toolkit-archive
下载NVIDIA驱动对应的cuda_10.0.130_410.48_linux.run文件: CUDA Toolkit 10.0 Archive -> Linux -> x86_64 -> Ubuntu -> 16.04 -> runfile(local)
sudo sh cuda_10.0.130_410.48_linux.run
* 安装:除以下选择为no,其他均为y及默认
> Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 361.62?
(y)es/(n)o/(q)uit: n
* 配置环境变量
~/.bashrc添加
```
export PATH=/usr/local/cuda-10.0/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```
* 查看是否安装成功
```
cd /usr/local/cuda-10.0/samples/1_Utilities/deviceQuery
sudo make
./deviceQuery
```
* 查看cuda版本
```
cat /usr/local/cuda-10.0/version.txt
```
### 3 安装cudnn 7.6.5
* 下载驱动（首次登录需注册并填问卷）
https://developer.nvidia.com/rdp/cudnn-archive
下载cudnn-10.0-linux-x64-v7.6.5.32.tgz压缩包[Download cuDNN v7.6.5 (November 5th, 2019), for CUDA 10.0 -> cuDNN Library for Linux]，大小为486MB
解压后生成cuda文件夹
```
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/*.* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```
* 查看cudnn版本（CUDNN_VERSION 7.6.5）
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2
