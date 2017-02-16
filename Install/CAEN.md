<!-- CAEN.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 日 4月 24 12:32:31 2016 (+0800)
;; Last-Updated: 四 2月 16 19:29:49 2017 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 27
;; URL: http://wuhongyi.cn -->

# CAEN 官方库安装

CAEN 官方提供了其产品的底层驱动、部分图形软件等。根据需要自行选择安装。

以下为基础驱动：  
- CAENVMELib
- CAENComm
- CAENUpgrader
- CAENDigitizer
- CAENUSBdrvB
- A2818Drv

以下为Digitizer获取的应用软件：  
- DPP-PHA_ControlSoftware
- DPP-PSD_ControlSoftware
- ZLEControlSoftware
- wavedump



----

## CAENVMELib-2.50

**该库VME、Digitizer获取均需要安装**

解压缩 CAENVMELib-2.50.tgz 文件。

执行lib文件夹下install_64文件

```bash
./install_x64
```

----

## CAENComm-1.2

**该库Digitizer获取需要安装**

解压缩 CAENComm-1.2-build20140211.tgz 文件。

执行lib文件夹下install_64文件

```bash
./install_x64
```

----

## CAENUpgrader-1.6.0

**该库VME、Digitizer获取均需要安装，用来升级固件**

解压缩 CAENUpgrader-1.6.0-build20161104.tgz 文件。

```bash
./configure
make
make install
```

----

## CAENDigitizer_2.7.6

**该库Digitizer获取需要安装**

解压缩 CAENDigitizer_2.7.6_20161014.tgz 文件

```bash
./install_x64
```

----

## USB 线连接 -- CAENUSBdrvB-1.5.1

**该库VME、Digitizer获取均需要安装，用来通过USB线传输数据**

解压缩 CAENUSBdrvB-1.5.1.tgz 文件。

```bash
make
make install
```

## 2818采集卡连接 -- A2818Drv-1.19-build20150826.tgz

**该库VME、Digitizer获取均需要安装，用来通过光纤传输数据**

```bash
#将该文件夹复制到 /opt 并安装在该位置
cp -r A2818Drv-1.19 /opt
cd /opt/A2818Drv-1.19
cp ./Makefile.2.6-3.x Makefile
make
#设置开机自动执行该脚本
emacs /etc/rc.local   ## 或 emacs /etc/rc.d/rc.local
#在最后添加 /bin/sh /opt/A2818Drv-1.19/a2818_load.2.6-3.x
```

----


## DPP-PHA_ControlSoftware-1.2.3

**该软件Digitizer获取需要安装，是针对PHA固件的软件**

解压缩 DPP-PHA_ControlSoftware-1.2.3.tar.gz 文件。

```bash
./configure
make
make install
```

## DPP-PSD_ControlSoftware-1.3.3

**该软件Digitizer获取需要安装，是针对PSD固件的软件**

解压缩 DPP-PSD_ControlSoftware-1.3.3.tar.gz 文件

```bash
./configure
make
make install
```

## ZLEControlSoftware-1.0.0

**该软件Digitizer获取需要安装，是针对ZLE固件的软件**

ZLEControlSoftware-1.0.0.tar.gz

```bash
./configure
make
make install
#Default config file is "/etc/ZLEControlSoftware/ZLEControlSoftwareConfig.txt"
```

## wavedump-3.7.2

**该软件Digitizer获取需要安装，是针对STD固件的软件，适用于大多硬件**

wavedump-3.7.2.tar.gz

```bash
./configure
make
make install
#Default config file is "/etc/wavedump/WaveDumpConfig.txt"
```

<!-- CAEN.md ends here -->
