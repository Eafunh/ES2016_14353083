#ROS安装文档
####14M1 14353083 何裕丰
***
##ROS
ROS(Robot Operating System）是一个机器人软件平台，它能为异质计算机集群提供类似操作系统的功能。

ROS提供一些标准操作系统服务，例如硬件抽象，底层设备控制，常用功能实现，进程间消息以及数据包管理。ROS是基于一种图状架构，从而不同节点的进程能接受，发布，聚合各种信息（例如传感，控制，状态，规划等等）。目前ROS主要支持Ubuntu。

##ubuntu14.04-32bit下安装ROS系统
###准备工作：
* 确保更新源universe、restricted、multiverse勾上
<img src="http://p1.bpimg.com/4851/4e1eda1fe535e101.png" alt="Software &amp; Updates">
* 设置系统，使其可以接受packages.ros.org的软件
```
sudo sh -c ‘echo “deb <a href="http://packages.ros.org/ros/ubuntu">http://packages.ros.org/ros/ubuntu</a> trusty main” &gt; /etc/apt/sources.list.d/ros-latest.list
```
* 设置Key
```
wget <a href="https://raw.githubusercontent.com/ros/rosdistro/master/ros.key">https://raw.githubusercontent.com/ros/rosdistro/master/ros.key</a> -O - | sudo apt-key add –
```
* 更新软件包的地址
```
  sudo apt-get update
```
<img src="http://p1.bpimg.com/4851/98f017537158ab8e.png" alt="更新包地址">

###下载安装
* 下载并安装ROS-indigo
```
sudo apt-get install ros-indigo-desktop-full
```
<img src="http://p1.bpimg.com/4851/cdaa01d5c165e781.png" alt="install">
* 查看可使用的包
```
apt-cache search ros-indigo
```
* 初始化ROS
```
sudo rosdep init
```
<img src="http://i1.piimg.com/4851/3170742ff4cbf2e6.png" alt="initial">
* 更新ROS
```
rosdep update
```
<img src="http://i1.piimg.com/4851/f978ac0d79531cd2.png" alt="update ros">
* 设置环境变量
```
echo "source /opt/ros/indigo/setup.bash" &gt;&gt; ~/.bashrc
source ~/.bashrc
```
注意：第一条命令中，很多网站给的是echo "source /opt/ros/jade/setup.bash" &gt;&gt; ~/.bashrc，结果发现并没有jade这一个目录，执行之前最好先确认下setup.bash的目录究竟是什么，如我的ubuntu里是indigo。如果第一条命令中的路径错了，将会在/.bashrc文件里添加了错误的路径，直接影响以后所有命令的执行。解决方法是sudo gedit ~/.bashrc打开bashrc，将错误的路径信息删掉，重新执行命令即可。

* 安装rosinstall
```
sudo apt-get install python-rosinstall
```
<img src="http://i1.piimg.com/4851/765539c79038f7ab.png" alt="rosinstall">
* 至此ROS安装完毕

###测试</h3>
* 根据下述网站安装驱动、执行命令测试
    >http://blog.csdn.net/u013793399/article/details/51831722

* 效果如下，可在终端窗口控制乌龟的运动：

<img src="http://i1.piimg.com/4851/1fffbd73f9cff190.png" alt="test">

##实验感想
这次实验总体来说并没有什么难度，纯粹跟着文档一步步执行命令即可，实际流程大概分为准备好更新的环境，下载并安装安装包，配置好环境变量，最后安装必要的工具和驱动，运行实例进行测试。
但依然会有一些小细节容易出差错，如设置环境变量过程中需要注意路径是否对应自己的实际路径。这告诉了我们，不能够直接复制粘贴就算了，要学会理解命令的含义和作用，更要学会从错误提示中找到解决方法。
