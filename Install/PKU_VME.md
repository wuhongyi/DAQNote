<!-- PKU_VME.md --- 
;; 
;; Description: 
;; Author: Hongyi Wu(吴鸿毅)
;; Email: wuhongyi@qq.com 
;; Created: 三 9月 21 09:23:05 2016 (+0800)
;; Last-Updated: 五 2月 17 21:23:30 2017 (+0800)
;;           By: Hongyi Wu(吴鸿毅)
;;     Update #: 13
;; URL: http://wuhongyi.cn -->

# PKU VME 获取

PKU VME 获取是基于 Riken DAQ 获取发展而来。


统安装完成之后，建议关闭防火墙：

```bash
su
setup
exit
```

----

## babirl安装

babirl下载地址：https://ribf.riken.jp/RIBFDAQ/index.php?DAQ%2FDownload

**当前只测试到150401版本，170125版为尚未测试。**

```bash
cp babirl* ~
tar zxvf babirl150401.tar.gz
ln -sf babirl150401 babirl
cd babirl
emacs include/userdefine.h
```

将文件中的内容修改如下：

```cpp
#define BABIRLDIR "/home/wuhongyi/babirl"
#define PIDDIR    "/home/wuhongyi/babirl/run"
// 这里wuhongyi为当前用户名
```

修改完成之后保存，编译并且添加开机自启动：

```bash
make
su
cp /home/wuhongyi/babirl/rcd/babimo /etc/init.d  #这里wuhongyi为当前用户名
ln -sf /etc/init.d/babimo /etc/rc2.d/S99babimo
ln -sf /etc/init.d/babimo /etc/rc3.d/S99babimo
ln -sf /etc/init.d/babimo /etc/rc5.d/S99babimo
emacs /etc/init.d/babimo
```

将DIR=/usr/babirl改成/home/wuhongyi/babirl  
同时修改wuhongyi和root的用户目录下的.bashrc文件，添加如下内容：（这里wuhongyi为当前用户名）

```bash
PATH=$PATH:/home/wuhongyi/babirl/bin/
#这里wuhongyi为当前用户名
```

检查如下内容：

```bash
dmesg|grep a2818
ps aux|grep babi*
exit
```

查看输出是否正常。


## caenvmebabies和cmdvme安装

bbcanvme/lib 将CAEN的官方库进行了一次封装，得到了一些函数名相对简化的函数。供babies、module和cmdvme使用。  
cmdvme使用了libbbcaenvme中的命令，可以读取或者写入插件某一个寄存器地址。  
module中各个插件调用了libbabies和libbbcaenvme来完成插件动作的定义。  
babies调用以上所有来完成event的构建。主要修改文件有start/evt/clear/stop的C文件。


```bash
cd ~
tar zxvf DAQ_CAEN_CBLT.tar.gz
cd bbcaenvme
cd cmdvme
make clean
make
cd ../babies
make clean
make
ln -sf caenvmebabies babies
```


## 连接VME机箱调试

A2818安装前确认电压+3.3V/+5V

V2718放在VME的第一个slot  
V2718PCB板上DIP开关：Prog0    off    1    off    2    off    3    on    4    off    I/O    NIM

./babies 10



运行babicon(安装后第一次需输入以下初始化)

```bash
seteflist 10 add localhost localhost
sethdlist 0 path /home/wuhongyi/data    #这里为数据存储路径
setclinfo 0 add localhost
setclinfo 0 id  0
```



## 安装 anaroot

```shell
$ tar -zxvf anaroot.tar.gz
$ cd anaroot
$ rm sources/Core/anacore_dict*
# 修改 CBLT.hh 文件，使得参数与获取插件对应
$ make clean
$ ./autogen.sh --prefix=$PWD
$ make
$ make install
```

在 .bashrc 中加入以下

```shell
export TARTSYS=/home/wuhongyi/anaroot
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$TARTSYS/lib:$TARTSYS/sources/Core
```

----

## 一些技巧及约定

硬件顺序：SDC、ADC、GDC、MADC

地址分配：V785: 0x1000开始、MADC32: 0x2000开始、V1190: 0x4000开始、V830: 0x5000开始。

GEO分配： ADC:0-19; MADC:20-39; GDC:40-49; SDC:50-59


查看有没有数据：  
```bash
chkridf -s 0
```

<!-- PKU_VME.md ends here -->
