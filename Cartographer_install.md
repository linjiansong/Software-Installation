参考 [Cartographer官网](https://google-cartographer.readthedocs.io/en/latest/)      [CSDN博客](https://blog.csdn.net/qq_42938987/article/details/106739233)
# 简介
Cartographer is a system that provides real-time simultaneous localization and mapping (SLAM) in 2D and 3D across multiple platforms and sensor configurations.

# Getting started without ROS
Please see our ROS integration as a starting point for integrating your system with the standalone library. Currently, it is the best available reference.

* 添加依赖项
```
sudo apt-get update
sudo apt-get install -y \
    clang \
    cmake \
    g++ \
    git \
    google-mock \
    libboost-all-dev \
    libcairo2-dev \
    libcurl4-openssl-dev \
    libeigen3-dev \
    libgflags-dev \
    libgoogle-glog-dev \
    liblua5.2-dev \
    libsuitesparse-dev \
    lsb-release \
    ninja-build \
    stow
```
* 安装abseil-cpp
```
git clone https://github.com/abseil/abseil-cpp.git
cd abseil-cpp
git checkout d902eb869bcfacc1bad14933ed9af4bed006d481
mkdir build
cd build
cmake -G Ninja \
  -DCMAKE_BUILD_TYPE=Release \
  -DCMAKE_POSITION_INDEPENDENT_CODE=ON \
  -DCMAKE_INSTALL_PREFIX=/usr/local/stow/absl \
  ..
ninja
sudo ninja install
cd /usr/local/stow
sudo stow absl

VERSION="1.13.0"
```

* 安装ceres
```
git clone https://ceres-solver.googlesource.com/ceres-solver
cd ceres-solver
git checkout tags/${VERSION}
mkdir build
cd build
cmake .. -G Ninja -DCXX11=ON
ninja
CTEST_OUTPUT_ON_FAILURE=1 ninja test
sudo ninja install

VERSION="v3.4.1"
```

* 安装protobuf
```
git clone https://github.com/google/protobuf.git
cd protobuf
git checkout tags/${VERSION}
mkdir build
cd build
cmake -G Ninja \
  -DCMAKE_POSITION_INDEPENDENT_CODE=ON \
  -DCMAKE_BUILD_TYPE=Release \
  -Dprotobuf_BUILD_TESTS=OFF \
  ../cmake
ninja
sudo ninja install
```

* 安装Cartographer
```
cd cartographer
mkdir build
cd build
cmake .. -G Ninja
ninja
CTEST_OUTPUT_ON_FAILURE=1 ninja test
sudo ninja install
```
# ROS中使用
* 安装cartographer_ros
```
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/src
catkin_init_workspace
echo "source catkin_ws/devel/setup.bash" >> ~/.bashrc(我使用的是zsh终端，如果为bash终端，则是setup.zsh和~/.bashrc)
source ~/.zshrc

cd ~/catkin_ws/src
git clone https://github.com/hitcm/cartographer_ros.git
cd ~/catkin_ws
catkin_make
```

* 测试
[2D数据集下载链接](https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/cartographer_paper_deutsches_museum.bag)
```
# 2D (第三个参数为下载数据集路径)
roslaunch cartographer_ros demo_backpack_2d.launch bag_filename:=${HOME}/Downloads/cartographer_paper_deutsches_museum.bag
# 3D (第三个参数为下载数据集路径)
roslaunch cartographer_ros demo_backpack_3d.launch bag_filename:=${HOME}/Downloads/cartographer_3d_deutsches_museum.bag
```
