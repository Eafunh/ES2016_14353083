# ES2016_14353083
**Course:** *Embedded System 2016* **Name:** *何裕丰* **SNO:** *14353083*
***
##Description  
The distributed operation layer (DOL) is a framework that enables the (semi-) automatic mapping of applications onto the multiprocessor SHAPES architecture platform. The DOL consists of basically three parts:

- **DOL Application Programming Interface:**   
Enable the programming of distributed, parallel applications for the SHAPES platform.
- **DOL Functional Simulation:**   
Be used to obtain performance parameters at the application level and  to provide programmers a possibility to test their applications.
- **DOL Mapping Optimization:**   
Compute a set of optimal mappings of an application onto the SHAPES architecture platform. 
![framework](http://p1.bpimg.com/4851/2816b7851abd9647.png)

##How to install
1. 搭建linux虚拟机  
用VMWare搭建Ubuntu系统虚拟机
2. 准备工具  
Make工具、Ant工具、Java  
        $   sudo apt-get update
        $   sudo apt-get install ant
        $   sudo apt-get install openjdk-7-jdk
        $   sudo apt-get install unzip

3. 解压dol、systemc文件  
        $   mkdir dol
        $   unzip dol_ethz.zip -d dol
        $   tar -zxvf systemc-2.3.1.tgz
4. 编译systemc
        $    cd systemc-2.3.1
        $    mkdir objdir
        $    cd objdir
        $    ../configure CXX=g++ --disable-async-updates
        $    sudo make install
5. 编译dol
进入dol文件夹，找到build_zip.xml文件，用gedit打开。  
找到下面这段话，将YYY改成systemc-2.3.1的路径，如 /root/systemc-2.3.1
        <property name="systemc.inc" value="YYY/include"/>
        <property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>
编译dol，若成功会出现build successful  
        `ant -f build_zip.xml all  
运行第一个例子，若成功会出现build successful
        $    cd build/bin/main
        $    ant -f runexample.xml -Dnumber=1
至此，dol配置完毕。

##Experimental experience
1. 由于上学期操作系统课程已经搭建好Ubuntu虚拟机，故这次配置DOL环境省下了不少时间。但纵使是早就接触了linux，对linux的各种命令依然是十分陌生，绝大多数时候都是百度，然后复制粘贴。  
2. 在配置的过程中，有可能出现无法下载或无法更新的问题，这可能是源的问题，在软件中心更换即可。
3. 对DOL的认识基本只知道其为分布式操作层及一些基本概念，其他全然不知，希望能在日后学习中能够熟练掌握。
4. 由于实验环境配置了很久之后才写这个配置文档，所以没有配置过程中的截图。
