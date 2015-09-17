title: Install-Torch-7-on-Ubuntu-14-04
date: 2015-09-17 10:24:51
categories: "Deep Learning"
tags: Torch
---

## Install
```
$> mkdir ~/torch
$> cd ~/torch
$> curl -s https://raw.githubusercontent.com/torch/ezinstall/master/install-deps | bash
$> git clone https://github.com/torch/distro.git ~/torch --recursive
$> ./install.sh
$> source ~/.bashrc
$> th
// If th run is ok, then install success.
```

## Reference
http://torch.ch/
http://torch.ch/docs/getting-started.html#_
