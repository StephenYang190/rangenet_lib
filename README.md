# Rangenet Library

This repository contains simple usage explanations of how the RangeNet++ inference works with the TensorRT and C++ interface.

Developed by [Xieyuanli Chen](https://www.ipb.uni-bonn.de/people/xieyuanli-chen/), [Andres Milioto](https://www.ipb.uni-bonn.de/people/andres-milioto/) and [Jens Behley](https://www.ipb.uni-bonn.de/people/jens-behley/).

Modified by Tongda Yang for tensorrt8.

My environment is:

```
Tensorrt = 8.0
CUDA drive = 11.2
CUDA running time = 11.1
cudnn = 8.2.1.32
ubuntu = 20.04
```


---
## How to use

#### Dependencies

#### CUDA Install

First you need prepare your nvidia driver and CUDA:

CUDA package on cdn: [Link](http://cdn.isus.tech/downloads/cuda/Ubuntu_2004/)

cudnn package on cdn: [Link](http://cdn.isus.tech/downloads/cudnn/2004/)

#### Tensorrt8 install

Then you need to install tensorrt8:

(We strongly recommend your install as following steps using tensorrt.tar)

1. Install tar package fit your environment

Official install link: [Link](https://developer.nvidia.com/nvidia-tensorrt-8x-download)

TensorRT GA is general availability.

TensorRT EA stands for early access.

We recommend you install GA version as the instruction of official tutorial.

2. Extract

   ```sh
   tar zxf TensorRT-8.0.1.6.Linux.x86_64-gnu.cuda-11.3.cudnn8.2.tar.gz
   ```

   move to the path you want to set

   ```sh
   mv TensorRT-8.0.1.6 /path/you/want/to/set
   ```

3. Set environment variable in ~/.bashrc

   ```sh
   export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/path/you/want/to/set/TensorRT-8.0.1.6/lib
   export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/path/you/want/to/set/TensorRT-8.0.1.6/targets/x86_64-linux-gnu/lib
   ```

   Remember to source your file

   ```sh
   source ~/.bashrc
   ```

   

4. Copy the lib and include to system

   ```sh
   sudo cp -r ./lib/* /usr/lib
   sudo cp -r ./include/* /usr/include
   ```

   

5. Test your tensorrt using official example

   example in TensorRT-8.0.1.6/samples/sampleMNIST

   ```sh
   make
   ```

##### System dependencies
You can do the other dependencies:

```sh
$ sudo apt-get update 
$ sudo apt-get install -yqq  build-essential python3-dev python3-pip apt-utils git cmake libboost-all-dev libyaml-cpp-dev libopencv-dev
```

##### Python dependencies

Then install the Python packages needed:

```sh
$ sudo apt install python-empy
$ sudo pip install catkin_tools trollius numpy
```

#### Build the library
We use the catkin tool to build the library.

  ```sh
  $ mkdir -p ~/catkin_ws/src
  $ cd ~/catkin_ws/src
  ```

Download this file in src directory

```sh
cd ~/catkin_ws
catkin init
catkin build rangenent_lib
```

#### Run the demo

You need to install the pre-trained darknet model. [Link](http://www.ipb.uni-bonn.de/html/projects/bonnetal/lidar/semantic/predictions/darknet53.tar.gz)

A single LiDAR scan for running the demo, you could find in the example folder `example/000000.bin`. For more LiDAR data, you could download from [KITTI odometry dataset](https://www.cvlibs.net/datasets/kitti/eval_odometry.php).

To infer a single LiDAR scan and visualize the semantic point cloud:

  ```sh
  # go to the root path of the catkin workspace
  $ cd ~/catkin_ws
  # use --verbose or -v to get verbose mode
  $ ./devel/lib/rangenet_lib/infer -h # help
  $ ./devel/lib/rangenet_lib/infer -p /path/to/the/pretrained/model -s /path/to/the/scan.bin --verbose
  ```

**Notice**: for the first time running, it will take several minutes to generate a `.trt` model for C++ interface.
