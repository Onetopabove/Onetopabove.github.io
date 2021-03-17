---
title: linux/Windows双系统共用蓝牙键盘
date: 2021-03-17 15:22:46
tag
---

### 参考文章

[Linux下调教Logitech K480蓝牙键盘](https://fspark.me/archives/regulate-logitech-k480.html)

[Ubuntu和Windows双系统连接罗技蓝牙键盘](https://blog.csdn.net/qq_33054139/article/details/86236053)

### 补充说明

#### **原理**

电脑与键盘都有一个蓝牙MAC地址，在电脑上的Windows/Linux上与一个键盘配对后，会随机产生一个Link Key。每一次MAC地址1与MAC地址2之间进行配对都会产生一个Link Key，这个Link Key会保存在操作系统与蓝牙键盘中。

要让同一键盘连接同意设备上的两个不同的操作系统，需要做的是将两个**操作系统中的Link Key**设为同一值，同时**键盘中保存的Link Key**也要相同，即三者的内容一致。

#### **操作流程**

1. 登录Linux系统，配对、连接蓝牙键盘，获取**键盘的MAC地址**并在Linux系统下建立一个配对文件（自动生成）。
2. 登录Windows系统，配对、连接蓝牙键盘（这时键盘内的Link Key发生了变化），获取**Windows生成的Link Key**。
3. 回到Linux下，**不再重新配对、连接**蓝牙键盘，可以连一个有线键盘，修改`/var/lib/bluetooth/电脑MAC/键盘MAC/info`里的Key值为**Windows生成的Link Key**。
4. 保存并重启蓝牙服务，按几下键盘即可连接成功。

这里的顺序：Linux-->Windows-->Linux，也可Windows-->Linux-->Windows。

### 需要用到的软件

[官网PSTools](https://docs.microsoft.com/zh-cn/sysinternals/downloads/psexec)或者[我下载好的](/download/PSTools)