# PIScope 的使用

本文主要简单介绍下PIScope的使用方法。

## 目录

0. [PISope安装](#PIScope安装)
0. [PIScope连接MDSPlus](#PIScope连接MDSPlus)
0. [PIScope简单可视化数据](#PIScope简单可视化数据)
0. [PIScope脚本式可视化数据](#PIScope脚本式可视化数据)

## PIScope安装

### Windows环境安装

> 1. 安装python，推荐选择[python2.7](https://www.python.org/downloads/windows/)，选择相应的版本并安装。
> 2. 安装MDSplus，推荐选择[stable版本](http://www.mdsplus.org/index.php/Latest_Windows_Distributions)，下载并安装。
> 3. 安装相应的python依赖包，这里选择清华pypi镜像安装：
```
  pip install numpy -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  pip install scipy -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  pip install PyPDF2 -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  pip install hgapi -i https://pypi.tuna.tsinghua.edu.cn/simple/
  pip install PyOpenGL -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  pip install H5py -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  pip install Pillow -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  pip install mdsplus -i https://pypi.tuna.tsinghua.edu.cn/simple/
  pip install netCDF4 -i https://pypi.tuna.tsinghua.edu.cn/simple/
  pip install matplotlib -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  pip install wxPython -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
```

### Ubuntu环境安装

> 1. 安装python
```
  sudo apt-get install python2.7
```
> 2. 安装MDSplus，按照下面命令安装，具体参看[安装教程](http://www.mdsplus.org/index.php/Latest_Ubuntu/Debian_Packages)。
```
  **注意：**os-selection为ubuntu版本，如：**Ubuntu14**，flavor选择**stable**或者**alpha**
  deb http://www.mdsplus.org/dist/os-selection/repo MDSplus flavor
  wget http://www.mdsplus.org/dist/mdsplus.gpg.key
  sudo apt-key add mdsplus.gpg.key
  sudo apt-get update
  sudo apt-get install mdsplus
```
> 3. 安装相应依赖包:

* 安装相应的ubuntu依赖包
```
  sudo apt-get install dpkg-dev
  sudo apt-get install build-essential
  sudo apt-get install python2.7-dev # 选择相应的版本
  sudo apt-get install libjpeg-dev
  sudo apt-get install libtiff-dev
  sudo apt-get install libsdl1.2-dev
  sudo apt-get install libgstreamer-plugins-base0.10-dev
  sudo apt-get install libnotify-dev
  sudo apt-get install freeglut3
  sudo apt-get install freeglut3-dev
  sudo apt-get install libsm-dev
  sudo apt-get install libgtk-3-dev
  sudo apt-get install libwebkitgtk-3.0-dev 
  sudo apt-get install libxtst-dev
```

* 安装python依赖包：
```
  sudo apt-get install python-numpy
  sudo apt-get install python-scipy
  sudo pip install PyPDF2 -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  sudo pip install hgapi -i https://pypi.tuna.tsinghua.edu.cn/simple/
  sudo pip install PyOpenGL -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  sudo pip install H5py -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  sudo pip install Pillow -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  sudo pip install mdsplus -i https://pypi.tuna.tsinghua.edu.cn/simple/
  sudo pip install netCDF4==1.4.0 -i https://pypi.tuna.tsinghua.edu.cn/simple/
  sudo pip install matplotlib==2.2.3 --ignore-installed six -i https://pypi.tuna.tsinghua.edu.cn/simple/ 
  #**注意：**安装wxPython包时，pip镜像源没有Linux版本的,这里选择官方给的安装方法。
  #安装wxPython时建议翻墙否则速度太慢。
  #这里“ubuntu-16.04”改成相应的Ubuntu版本
  pip install -U -f https://extras.wxpython.org/wxPython4/extras/linux/gtk3/ubuntu-16.04 wxPython
```

### 运行PIScope

> 1. 下载PIScope
```
  git clone https://github.com/sshiraiwa/piScope.git
```
> 2. 启动PIScope
```
  cd $PISCOPE_DIR
  python python/piscope.py
```

## PIScope连接MDSPlus

> 1. 创建一个Scope
```
  #在交互式窗口输入scope()命令
  >>scope()
```

![Scope窗口](https://github.com/shenzhengyang/PIScope/blob/master/img/1.png)

> 2. 点击scope->global setting->config，打开MDSplus服务器配置选项卡

![config选项卡](https://github.com/shenzhengyang/PIScope/blob/master/img/2.png)

> 3. 创建个新的连接服务器

![创建新服务器](https://github.com/shenzhengyang/PIScope/blob/master/img/3.png)

## PIScope简单可视化数据

> 1. 在Scope窗口点击右键->Add MDS Session

![添加Session](https://github.com/shenzhengyang/PIScope/blob/master/img/9.png)

> 2. 填写Tree、Node名称

![添加Tree](https://github.com/shenzhengyang/PIScope/blob/master/img/4.png)
![填写Node](https://github.com/shenzhengyang/PIScope/blob/master/img/5.png)

> 3. 填写shot号

![填写shot](https://github.com/shenzhengyang/PIScope/blob/master/img/6.png)

## PIScope脚本式可视化数据

> 1. 在交互式终端编写脚本
```
>> from MDSplus import Connection     #导入连接MDSplus包
>> c=Connection('202.127.204.12')     #连接MDSplus
>> c.openTree('EAST',50000)           #打开Tree，'EAST'树名称，50000炮号
>> ipm=c.get('\EAST::TOP.T1:IPM')     #获得一个Node
>> ipm=ipm.data()                     #获取Node数据
>> ipm_time=c.get('dim_of(\EAST::TOP.T1:IPM)') #获取时间序列
>> from ifigure.interactive import *  #导入PIScope画图包
>> v=figure(proj.book)                #创建一个figure
>> v.addpage()                        #添加一个page
>> plot(ipm_time,ipm)                 #绘制图形
```

![脚本](https://github.com/shenzhengyang/PIScope/blob/master/img/7.png)
![绘图](https://github.com/shenzhengyang/PIScope/blob/master/img/8.png)

## 总结

PIScope的使用方法和matlab很相似，有matlab基础的可能感觉不陌生。
