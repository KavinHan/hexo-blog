title: Ubuntu14.04 安装 Torch 7
date: 2015-09-17 10:24:51
categories: "Deep Learning"
tags: Torch
---

## 安装
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

## 参考
- http://torch.ch/
- http://torch.ch/docs/getting-started.html#_
