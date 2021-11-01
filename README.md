# Rangenet Library

This repository contains simple usage explanations of how the RangeNet++ inference works with the TensorRT and C++ interface.

Developed by [Xieyuanli Chen](https://www.ipb.uni-bonn.de/people/xieyuanli-chen/), [Andres Milioto](https://www.ipb.uni-bonn.de/people/andres-milioto/) and [Jens Behley](https://www.ipb.uni-bonn.de/people/jens-behley/).

For more details about RangeNet++, one could find in [LiDAR-Bonnetal](https://github.com/PRBonn/lidar-bonnetal).

Modified by Tongda Yang for tensorrt8.

My environment is:

```
Tensorrt 8.0
CUDA drive 11.2
CUDA running time 11.1
cudnn 8.2.1.32
ubuntu 20.04
```



<p align="center">
  <img width="460" height="300" src="pics/demo.png">
</p>

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
   sudo cp -r ./include/* /user/include
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

A pre-trained model darknet have installed in the directory rangenet_lib/darknet/

A single LiDAR scan for running the demo, you could find in the example folder `example/000000.bin`. For more LiDAR data, you could download from [KITTI odometry dataset](https://www.cvlibs.net/datasets/kitti/eval_odometry.php).

For more details about how to train and evaluate a model, please refer to [LiDAR-Bonnetal](https://github.com/PRBonn/lidar-bonnetal).

To infer a single LiDAR scan and visualize the semantic point cloud:

  ```sh
  # go to the root path of the catkin workspace
  $ cd ~/catkin_ws
  # use --verbose or -v to get verbose mode
  $ ./devel/lib/rangenet_lib/infer -h # help
  $ ./devel/lib/rangenet_lib/infer -p /path/to/the/pretrained/model -s /path/to/the/scan.bin --verbose
  ```

**Notice**: for the first time running, it will take several minutes to generate a `.trt` model for C++ interface.

## Applications
#### Run SuMa++: Efficient LiDAR-based Semantic SLAM
Using rangenet_lib, we built a LiDAR-based Semantic SLAM system, called SuMa++.

You could find more implementation details in [SuMa++](https://github.com/PRBonn/semantic_suma/).

#### Generate probabilities over semantic classes for OverlapNet
OverlapNet is a LiDAR-based loop closure detection method, which uses multiple cues generated from LiDAR scans.

More information about our OverlapNet could be found [here](https://github.com/PRBonn/OverlapNet).

One could use our rangenet_lib to generate probabilities over semantic classes for training OverlapNet.

More detailed steps and discussion could be found [here](https://github.com/PRBonn/rangenet_lib/issues/31).

## Citations

If you use this library for any academic work, please cite the original [paper](https://www.ipb.uni-bonn.de/wp-content/papercite-data/pdf/milioto2019iros.pdf).

```
@inproceedings{milioto2019iros,
  author    = {A. Milioto and I. Vizzo and J. Behley and C. Stachniss},
  title     = {{RangeNet++: Fast and Accurate LiDAR Semantic Segmentation}},
  booktitle = {IEEE/RSJ Intl.~Conf.~on Intelligent Robots and Systems (IROS)},
  year      = 2019,
  codeurl   = {https://github.com/PRBonn/lidar-bonnetal},
  videourl  = {https://youtu.be/wuokg7MFZyU},
}
```

If you use SuMa++, please cite the corresponding [paper](https://www.ipb.uni-bonn.de/wp-content/papercite-data/pdf/chen2019iros.pdf):

```
@inproceedings{chen2019iros, 
  author    = {X. Chen and A. Milioto and E. Palazzolo and P. Giguère and J. Behley and C. Stachniss},
  title     = {{SuMa++: Efficient LiDAR-based Semantic SLAM}},
  booktitle = {Proceedings of the IEEE/RSJ Int. Conf. on Intelligent Robots and Systems (IROS)},
  year      = {2019},
  codeurl   = {https://github.com/PRBonn/semantic_suma/},
  videourl  = {https://youtu.be/uo3ZuLuFAzk},
}
```

## License

Copyright 2019, Xieyuanli Chen, Andres Milioto, Jens Behley, Cyrill Stachniss, University of Bonn.

This project is free software made available under the MIT License. For details see the LICENSE file.
