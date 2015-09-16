title: Install-Theano-on-Ubuntu-14-04
date: 2015-09-16 12:11:43
categories: "Deep Learning"
tags: "Theano"
---
*Theano version: 0.7*
## Install requirements
```
$> sudo apt-get install python-numpy python-scipy python-dev python-pip python-nose g++ libopenblas-dev git
$> sudo pip install Theano
$> cd ~/Downloads
$> git clone git://github.com/Theano/Theano.git
$> cd Theano
$> python setup.py develop --user
$> cd ..
```

## Test the newly installed packages
* NumPy (~30s):
```
python -c "import numpy; numpy.test()"
```
* SciPy (~1m):
```
python -c "import scipy; scipy.test()"
```
* Theano (~30m):
```
python -c "import theano; theano.test()"
```

## Reference
* http://deeplearning.net/software/theano/
* http://deeplearning.net/software/theano/install.html#install
* http://deeplearning.net/software/theano/install_ubuntu.html#install-ubuntu
