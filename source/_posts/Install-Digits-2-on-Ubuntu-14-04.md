title: Install-Digits-2-on-Ubuntu-14-04
date: 2015-09-16 10:29:51
categories: "Deep Learning"
tags: "Digits"
---

## Download [Digits 2.0](https://developer.nvidia.com/digits)
* Login NVidia
* Download DIGITS v2.0.0 for Ubuntu 14.04 to ~/Downloads

## Unpack the archive
```
$> cd ~/Downloads
$> tar xvf digits-2.0.tar.gz
```

## Install requirements
>The install.sh script installs all the requirements for DIGITS to run on Ubuntu 14.04. You only need to run this script once.

```
$> cd digits-2.0
$> ./install.sh
```

## Start DIGITS
>Use the runme.sh script to start the DIGITS server.

```
$> ./runme.sh
```

>Navigate in your browser to http://localhost:5000/ to view your webserver.

## Reference
* https://developer.nvidia.com/digits
* https://github.com/NVIDIA/DIGITS/releases/tag/v2.0.0
* https://github.com/NVIDIA/DIGITS/blob/digits-2.0/docs/WebInstall.md
* https://github.com/NVIDIA/DIGITS/blob/digits-2.0/docs/GettingStarted.md
* https://github.com/NVIDIA/DIGITS/blob/digits-2.0/README.md#installation
