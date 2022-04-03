---
layout: post
title:  "Downgrade the gcc version to version 5.5 on Ubuntu 18.04"
description: "Instructions to downgrade the gcc version to version 5.5"
date:   2022-04-03
categories: Ubuntu
---

First check existing gcc version, the default is 7.3 on Ubuntu 18.04
```shell
$ gcc --version
gcc (Ubuntu 7.3.0-27ubuntu1~18.04) 7.3.0
```
<br>

1. Download gcc/g++ 5
```shell
sudo apt-get install -y gcc-5
sudo apt-get install -y g++-5
```
2. Link gcc/g++ to downgrade
```shell
cd /usr/bin
sudo rm gcc
sudo ln -s gcc-5 gcc
sudo rm g++
sudo ln -s g++-5 g++
```
3. Check the gcc version again and you can see that it has been downgraded.
```shell
$ gcc --version
gcc (Ubuntu 5.5.0-12ubuntu1) 5.5.0 20171010
```

<br>
<b>Important: To revert above actions</b>
```shell
cd /usr/bin
sudo rm gcc
sudo ln -s gcc-7 gcc
sudo rm g++
sudo ln -s g++-7 g++
```