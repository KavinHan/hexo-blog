title: Ubuntu14.04 安装 Theano
date: 2015-09-16 12:11:43
categories: "Deep Learning"
tags: "Theano"
---
*Theano version: 0.7*
## 依赖
```
$> sudo apt-get install python-numpy python-scipy python-dev python-pip python-nose g++ libopenblas-dev git
$> sudo pip install Theano
$> cd ~/Downloads
$> git clone git://github.com/Theano/Theano.git
$> cd Theano
$> python setup.py develop --user
$> cd ..
```

## 测试
- NumPy (~30s):
```
python -c "import numpy; numpy.test()"
```
- SciPy (~1m):
```
python -c "import scipy; scipy.test()"
```
- Theano (~30m):
```
python -c "import theano; theano.test()"
```

## 参考
- http://deeplearning.net/software/theano/
- http://deeplearning.net/software/theano/install.html#install
- http://deeplearning.net/software/theano/install_ubuntu.html#install-ubuntu
