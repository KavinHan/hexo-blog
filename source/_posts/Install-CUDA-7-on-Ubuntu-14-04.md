title: Install-CUDA-7-on-Ubuntu-14-04
date: 2015-09-15 20:56:22
categories: "Deep Learning"
tags: "caffe"
---
# Install Caffe on Ubuntu 14.04

## Hardware Detail
* CPU: E5-2630
* RAM: 16GB
* GPU: GTX 960
* Hard Disk: 1TB

## Software Detail
* NVidia Driver : NVIDIA-Linux-x86_64-352.41.run.
* CUDA : cuda_7.0.28_linux.run
* cuDNN :  cudnn-7.0-linux-x64-v3.0-prod
* OpenBLAS : 0.2.14
* Boost : 1.54
* OpenCV : 3.0
* Python : 2.7
* Caffe : master branch

<!-- more -->

# Install Ubuntu 14.04

## Make usb Installer

## UEFI mode start ubuntu 14.04 usb installer

## Partition
* /boot : (efi) 500MB
* / : (ext4) 300GB //*if reinstall system, just format this partition*
* swap : (swap) 16GB //*just same with your RAM*
* /data : (ext4) 600+GB //*this partition write your self and It's for save training data*

## Install grub on /boot partition

# Install CUDA 7.0

## pre-install
```
$> sudo apt-get update
$> sudo apt-get install build-essential vim git
```

## Download
* Download [NVidia driver](http://www.nvidia.co.kr/Download/index.aspx) to ~/Download
* Download [CUDA run file installer bin file](https://developer.nvidia.com/cuda-downloads) to ~/Download

## Ready to install
```
$> cd ~/Downloads
$> sudo chmod +x NVIDIA-Linux-x86_64-352.41.run
$> ./cuda_7.0.28_linux.run -extract=~/Downloads/cuda_install
```

## Clear pre-install driver
```
// remove prev installed nvidia driver
$> sudo apt-get --purge remove nvidia-*

// disabled the Nouveau driver
$> sudo vim /etc/modprobe.d/blacklist.conf
$> (add new line at the end, and add this code) blacklist nouveau
$> sudo reboot
```

## Install NVidia driver
```
// After rebooting, Please directly switched to the terminal (using Ctrl + Alt + F1) and killed the X server to install the Nvidia driver
$> sudo service lightdm stop

// Install NVidia driver step: Accept >>> Continue installation >>> Install without signing >>> if warning just OK >>> OK >>> YES >>> OK >>>
$> sudo ~/Downloads/NVIDIA-Linux-x86_64-352.41.run
$> sudo modprobe nvidia
```

## Install CUDA 7.0.28
```
$> cd ~/Downloads/cuda_install
// Install step: accept >>> Enter >>> Enter >>> Enter
$> sudo ./cuda-linux64-rel-7.0.28-19326674.run
$> sudo ./cuda-samples-linux-7.0.28-19326674
```

## Test
```
//To test the installation
$> cd /usr/local/cuda/samples
$> cd 1_utilities/deviceQuery
$> sudo make
$> sudo ./deviceQuery
// If get Result PASS then install success
```

## Setting Environment
```
$> sudo service lightdm start
$> vim .bashrc
// add this two line to the end
export PATH=/usr/local/cuda-7.0/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-7.0/lib64:$LD_LIBRARY_PATH
$> source .bashrc
$> nvcc -V
// If get cuda version then set environment success
```

# Install cuDNN 7.0

## Install
```
// Register NVidia id first
Download cuDNN to ~/Downloads
$> sudo cp cuda/include/cudnn.h /usr/local/cuda/include/
$> sudo cp cuda/lib64/* /usr/local/cuda/lib64/
$> sudo ldconfig /usr/local/cuda/lib64/
```

# Install OpenCV 3.0

## Download
* Download [OpenCV3.0 for Linux/Mac](http://opencv.org/downloads.html) to ~/Downloads

## Install requirement
```
$> sudo apt-get -y install libopencv-dev cmake libgtk2.0-dev pkg-config python-dev python-numpy libdc1394-22 libdc1394-22-dev libjpeg-dev libpng12-dev libtiff4-dev libjasper-dev libavcodec-dev libavformat-dev libswscale-dev libxine-dev libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libtbb-dev libqt4-dev libfaac-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils unzip
```

##Unzip
```
$> cd ~/Downloads
$> unzip opencv-3.0.0.zip
```

## Compile
```
$> mv opencv-3.0.0.zip ~/
$> cd ~/opencv-3.0.0
$> mkdir build
$> cd build
$> cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D WITH_TBB=ON -D BUILD_NEW_PYTHON_SUPPORT=ON -D WITH_V4L=ON -D INSTALL_C_EXAMPLES=ON -D INSTALL_PYTHON_EXAMPLES=ON -D BUILD_EXAMPLES=ON -D WITH_QT=ON -D WITH_OPENGL=ON -D ENABLE_FAST_MATH=1 -D CUDA_FAST_MATH=1 -D WITH_CUBLAS=1 ..
// If Error: ...libGL.so...
$> sudo rm /usr/lib/x86_64-linux-gnu/libGL.so
$> sudo ln -s /usr/lib/libGL.so.1 /usr/lib/x86_64-linux-gnu/libGL.so
$> make -j $(nproc)
```

## Install
```
$> sudo make install
$> sudo /bin/bash -c 'echo "/usr/local/lib" > /etc/ld.so.conf.d/opencv.conf'
$> sudo ldconfig
```

## Test
```
$> cd ~/opencv-3.0.0/samples/
$> sudo cmake .
$> sudo make -j $(nproc)
$> cd cpp/
$> ./cpp-example-facedetect ../data/lena.jpg
// If show circle on lena face, then install success
```

# Install OpenBLAS and Boost

## Install OpenBLAS
```
$> sudo apt-get install gfortran
$> cd ~/Downloads
$> git clone git://github.com/xianyi/OpenBLAS
$> cd OpenBLAS
$> make -j $(nproc)
$> sudo make PREFIX=/usr/local install
```

## Install Boost
```
$> sudo apt-get install libboost-all-dev
```

# Install Caffe Require package

## Install protobuf, glog, gflags
```
$> sudo apt-get install libprotobuf-dev libgoogle-glog-dev libgflags-dev protobuf-compiler
```

## Install IO library: hdf5, leveldb, snappy, lmdb
```
$> sudo apt-get install libhdf5-serial-dev libleveldb-dev libsnappy-dev liblmdb-dev
```

## Install pip
```
$> sudo apt-get install python-pip
$> curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
$> sudo python get-pip.py
$> pip -V
```

## Install scipy
```
$> sudo apt-get install python-scipy
```


# Install Caffe

## Download
```
$> cd ~/Downloads
$> git clone https://github.com/BVLC/caffe.git
```

## Install
```
$> mv caffe/ ~/
$>  cd ~/caffe/
$> cp Makefile.config.example Makefile.config
$> sed -i 's/# USE_CUDNN := 1/USE_CUDNN := 1/' Makefile.config
$> sed -i 's/BLAS := atlas/BLAS := open/' Makefile.config
$>  for req in $(cat python/requirements.txt); do pip install $req; done
$> sudo pip install -r python/requirements.txt
$> make all -j $(nproc)
```
**If make error: cv::imread(cv::String const&, int)' .build_release/lib/libcaffe.so:.....**
**[Solution link](https://github.com/BVLC/caffe/issues/2348)**
> I meet the same problem and make a solution. add "opencv_imgcodecs" in Makefile.(LIBRARIES += glog gflags protobuf leveldb snappy \ lmdb boost_system hdf5_hl hdf5 m \opencv_core opencv_highgui opencv_imgproc opencv_imgcodecs) If you input "make all",the problem is the same again.But if you delete all the file in build(rm -rf ./build/*) before "make all",you will success

```
$> make pycaffe -j $(nproc)
$> echo "export CAFFE_ROOT=$(pwd)" >> ~/.bashrc
$> echo 'export PYTHONPATH=$CAFFE_ROOT/python:$PYTHONPATH' >> ~/.bashrc
$> source ~/.bashrc
```

## Test
```
$> ipython
$> import caffe
// If no error then install success
```

# Reference:

## Install CDUA
http://davidstutz.de/better-late-than-never-installing-cuda-and-caffe-on-ubuntu-14-04/
http://developer.download.nvidia.com/compute/cuda/7_0/Prod/doc/CUDA_Getting_Started_Linux.pdf

## Install cuDNN
http://www.cc.gatech.edu/~zk15/deep_learning/CUDAInstallationInstructions.txt

## Install OpenBLAS
https://github.com/tiangolo/caffe/blob/ubuntu-tutorial-b/docs/install_apt2.md

## Install Boost
https://github.com/tiangolo/caffe/blob/ubuntu-tutorial-b/docs/install_apt2.md

## Install OpenCV 3.0
http://rodrigoberriel.com/2014/10/installing-opencv-3-0-0-on-ubuntu-14-04/
http://blog.aicry.com/ubuntu-14-04-install-opencv-with-cuda/
http://sysads.co.uk/2014/05/install-opencv-2-4-9-ubuntu-14-04-13-10/
error: Problem with libGL.so on 64-bit Ubuntu

## Install Caffe:
https://github.com/tiangolo/caffe/blob/ubuntu-tutorial-b/docs/install_apt2.md
http://caffe.berkeleyvision.org/installation.html


tiff error, => ubuntu 14.04 not have tiff, so need compile opencv
opencv compile error =>
https://github.com/BVLC/caffe/issues/1559

http://www.rthpc.com/plus/view.php?aid=356
http://www.rthpc.com/plus/view.php?aid=375
http://docs.nvidia.com/cuda/cuda-getting-started-guide-for-linux/index.html#ubuntu-installation
http://developer.download.nvidia.com/compute/cuda/6_5/rel/docs/CUDA_Getting_Started_Linux.pdf
http://www.tuicool.com/articles/vimi6vOpenBLAS编译和安装简介
http://www.cnblogs.com/platero/p/3993877.htmlCaffe + Ubuntu 14.04 64bit + CUDA 6.5 配置说明


http://www.csdn.net/article/2015-01-22/2823663Caffe 深度学习框架上手教程

http://www.samontab.com/web/2014/06/installing-opencv-2-4-9-in-ubuntu-14-04-lts/


http://davidstutz.de/better-late-than-never-installing-cuda-and-caffe-on-ubuntu-14-04/

## install pip:
http://www.saltycrane.com/blog/2010/02/how-install-pip-ubuntu/


## install python:
http://askubuntu.com/questions/542171/how-to-install-scipy-with-pip3
http://stackoverflow.com/questions/24808043/importerror-no-module-named-scipy


## Tutorial:
http://www.joyofdata.de/blog/gpu-powered-deeplearning-with-nvidia-digits/

## make caffe error:
```
cv::imread(cv::String const&, int)' .build_release/lib/libcaffe.so:.....
//https://github.com/BVLC/caffe/issues/2348
```

## install pip on ubuntu 14.04
http://www.liquidweb.com/kb/how-to-install-pip-on-ubuntu-14-04-lts/

## install scipy on ubuntu 14.04
http://stackoverflow.com/questions/14408123/installing-scipy-on-ubuntu
