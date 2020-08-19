---
title: Linux常用命令总结
date: 2019-03-12 20:12:51
tags:
---

#### 1.virtualbox两种主要的网络连接方式

nat：虚拟机分配IP：10.0.2.15（255.255.255.0），网关是：10.0.2.2
虚拟机没有在本地局域网中占IP。实体机通过学校认证之后，虚拟机可以直接上网。

桥接：实体机和虚拟机在同一IP段。比如在1407教室里。172.17.6.x（255.255.255.0）：
实体机和虚拟机需要分别通过学校的认证才能上网。

#### 2.验证一下当前的IP

Windows： ipconfig ipconfig /all
Linux：   ifconfig ip a
centos：可能需要，在界面先连接“PCI以太网”

#### 3.备份虚拟机的硬盘

##### shell

windows:cmd.exe powershell.exe
linux: Bash

#### 查看当前用的那种shell

##### env

输出信息有：
SHELL=/bin/bash

### 常用命令

#### ls:列出文件（list）

常见用法：
ls-ls  //列出详细信息
0 drwxrwxr-x. 2 caidao caidao 6 3月 6 10:37 123
第一个d：代表目录
第一组rwx：表示所有者可读，写，执行
第二组rwx：表示同组用户可读，写，执行
第三组r-x：表示其它用户可读，不能写，可执行。
caidao caidao：表示该目录属于caidao这个用户，同时属性caidao这个组。
时间：表示文件最后访问时间
123：目录名

#### cat：输出文本文件的内容

##### 常见用法：

cat 文件名
cat 路径/路径/文件名

#### cd：改变当前路径的，进入某个目录

##### 常见用法：

cd 123		   进入当前目录下的123	<a href="123.jsp>链接</a>
cd ./123		与上面一样				<a href="./123.jsp>链接</a>
cd /  		      进入根目录				<a href="/">首页</a>
cd /home	      进入根下面的home		
cd ..			回到上一层目录		<a href="../">aa</a>
cd ../../		   回到上一层的上一层	<a href="../../">aa</a>
cd ../abc		去到与当前目录同级的abc里 <a href="../abc">aa</a>
cd ~			回家	
cd ~/		       回家					
				

pwd：查看当前路径

tree：以树型方式显示目录结构（没有这个命令，先安装sudo yum -y install tree）

#### mkdir：创建目录

##### 常见用法：

mkdir abc		       在当前目录下创建adc目录
mkdir ~/abc		   在自己家里创建abc:/home/user/abc
mkdir -p ~/abc/de 	在自己家里先创建abc，然后在abc下创建de

#### tar：用来压缩，解压，打包，解包的

打包：tar cvf 生成的包的名字.tar目录名
解包：tar xvf 包的名字.tar

测试的步骤
1.先在目录里建一个文本文件
2.打包
3.把目录改个名字
4.解包
5.比较目录里的文件对不对

帮助记忆：
c:创建
z:压缩，并且使用gz算法；
v：处理的时候，有信息才显示出来；
f.验证
x.解包
每个命令一般都加vf
c和x冲突的，只能加一个
带z的指令都用压缩有关

#### zxvf解压缩包

如果文件的后缀名是.tar 说明他是？
如果文件后缀名是.tar.gz 说明他是？

#### 下载

wget http://mirror.bit.edu.cn/apache/httpd/httpd/httpd-2.4.25.tar.gz

#### cp:复制文件或目录

用法：
cp 1.txt 2.txt
cp -r 要复制的目录 新目录

ln:创建链接（相当于windows下的“快捷方式”）
例如：
cd ~/桌面
ln -s/usr/bin/java	//这样在桌面上创建一个java的“快捷方式”
					//-表示创建软链接
ls-ls				//可以观察一下java这个文件的信息

#### touch：创建一个文件，更新创建时间和访问时间

例如：
touch scitc.txt

#### su:切换身份

例如：
su root				//切换成root用户
					//观察切换成root之后的提示符
					//输入root的密码
su caidao					//切换成caidao

sudo：不切换身份，但以root身份运行程序
例如：
mkdir /123			//权限不够，执行不了
sudo mkdir /123		//这样权限够，提示输入密码，输入当前用户的密码

top：查看系统资源

#### du：查看文件或者目录的大小

常见用法：
du：					//查看当前目录下的文件大小
du -h 				//同上，它k,m,g这些单位
du -h /  			//查看根目录下的文件或者目录大小
					//这个命令会运行很久，他要计算每一层
du -h -d 1 ~		//计算“自己家”目=目录和文件的大小。
					//只输出一层的结果
					
思考：要统计“桌面”目录的大小，参数要怎么写？

#### uname：输出系统信息

常见用法：
uname -a			//可以看出Linu内核版本，发布时间，机器名称等
					//不可以看到centos的版本
cat /etc/redhat-release  //kan centos的版本

exit：退出bash，关闭窗口



hostname：输入计算机名称
改名字：
hostnamectl set-hostname 名字

passwd：改密码

#### rm：删文件或者目录

常见用法
rm 文件名
rm -r 目录名
rm -rf 目录或者文件

mv：移动或者重命名
mv 老的目录或者文件 新的目录或者文件

4.目录结构



#### vim

1.启动
vim
vim 文件名   #文件可以存在，也可以不存在

2.vim工作模式
（1）普通模式
（2）编辑模式
（3）命令模式

3.切换工作模式
普通->编辑(i,a,I,A)
普通->命令（：）
编辑->普通（ESC）

4.常用的快捷键或者命令
：q			#退出
：w			#保存
：w 文件名	#保存，并指定一个名字
：wq			#保存并退出
：q!			#退出但不保存
dd			#删除一整行
qq			#光标移动到文件头部
G			#光标移动到文件结尾

5.杀进程
sudo kill 数字
sudo kill -9 数字

#### 创建用户

useradd -d/user/sam -m aam			#-d指定home，
					#-m是创建家目录
useradd -s /bin/sh -g group -Gadm,root gem     	#-s指定shell
                                              		 	#-g组的id
                                              			#-G是附加组

#### 删除用户

userdel [-r] 用户名               #-r删除用户的同时，把家目录删了

#### 修改密码

sudo    paswd    用户名        #修改别人的密码一定要用root;

#### 增加用户组

groupadd soft 组名

#### 删除组名

groupdel  组名

#### 修改用户所属组

usermod -g group（组名） loginname（登录名）
强行设置某个用户的主要组

usermod -G groups longinname
设置用户的附加组（把以前的附加组都去掉，只留设置的当前组）

usermod -a -G groups loninname
把用户添加进入某个附加组（之前有的组不变，在后面增加）

#如果用户不能使用sudo，可以把用户加到wheel组
sudo usermod -a -G wheel abc

#### 查询用户的组

groups 用户名                             // 查询用户的组
cat     /etc/group                       //查询系统所有组
cat     /etc/passwd                     //查询系统用户

chown 的用法，用来更改文件或者目录的所有者和组
chown [-r] 用户名：组名 文件或者目录名

#### chmod的用法，用来更改文件或者目录的权限

chmod     [R]     权限 文件名或者目录名
例如：
chmod     +x 1.txt               	#让所有者，同组用户，其他用户都可以执行1.txt
chmod     -w  2.txt              	#让所有者，同组用户，其他用户都不可以写2.txt
chomd     u-w 3.tx             	 #让所有者不能写3.txt，+或者-前面可以是u（所有者）
                               	       	o(其他用户)，g（同组用户）+代表给权限，-代表收回权限
chomd  g+rwx 4.txt           	  #一次给多个权限
chomd  oug+rwx 5.txt        	 #相当于777
chomd  124 5.txt                 	#第一位是1，代表所有者可执行
			#第二位是2，代表同组用户可写
			#第三位是4，代表其它用户可以读
			#1,2,4三个数字可以组合，比如3=2+1 表示可写可执行
			7=1+2+4，表示全部都可以



#### 分区管理(fdisk)

fdisk 硬盘的名字
(1)列出分区(p)
(2)删分区(d)
(3)建分区表(g:创建gpt分区表；m:创建mbr的分区表)
(4)建分区(n)

#### 管理文件系统(mkfs，mkswap，swapon，swapoff，mount，umount)

##### 创建文件系统

mkfs -t ext3 /dev/sdb1
mkswap /dev/sdb5 (在指定分区上创建交换文件系统、将/dev/sdb5格式转换为swap交换文件系统)
free | grep -i swap (通过free命令观察交换空间的变化)
swapon /dev/sdb5 (启用新的交换分区)
swapoff /dev/sdb5 (停用交换分区)

##### 挂载卸载文件系统

mount [-t 文件系统类型] 存储设备 挂载点
mount /devrom /media/cdrom (插入RHEL5光盘，并挂载到/media/cdrom中)
mount /dev/sdc1 /media/usbdsk (插入一个U盘，将其挂载到/media/usbdsk，挂载点需要事先创建好)
mount (直接输入也可查看系统中已挂载的各分区信息)
mount -o loop *****.iso /media/ubuntu (将下载的ISO镜像文件挂载到/media/ubuntu下)
umount /media/usbdsk (卸载已挂载到/media/usbdsk目录下的U盘文件系统)
eject和eject -t (对于光驱设备来说，前者是弹出托架、后者是收回托架)
cat /etc/fstab (/etc/fstab文件可以视为mount命令的配置文件、系统每次开机时会自动读取这个文件的配置)



##### 显示单个环境变量

echo $xxx

##### 设置一个新的环境变量hello,并且显示出来（注意大小书写）

$ export HELLO="Hello!"
echo $HELLO

##### 显示素有环境变量

env

##### 清除环境变量

unset

##### 环境变量种类

临时的，永久的

##### 设置永久变量的几个文件

/etc/profile 对所有的用户生效
~/.bash_profile 对单一用户生效（当前用户）
~/.bashrc 对单一用户生效，子bash启动才生效
/ect/bashrc也同样，只是全局的

7、修改两个profile之后，如果不想重启，可以执行下面的命令
source 文件名让它立即生效，如果改了bashrc文件，也可以用source来重新加载，也可以关闭了终端，重新打开，不需要重启



#### 设置静态IP地址

1.备份/etc/sysconfig/network-scropts/ifcfg-*,每个虚拟机的
2.vim etc/sysconfig/network-scripts/ifcfg-*
3.将BOOTPROTO=DHCP改为：BOOTPROTO=static,
4.增加：IPADDR=192... NETMASK=255... GATEWAY=192...
5.改DNS， 在/etc/sysconfig/network中增加：
6.第一行：DNS1=61.139.2.69 第二行：DNS=114.114.114.114
7.重启网络服务 service network restart
8.查看IP地址是否正确 ifconfig
9.检查网络是否通ping www.qq.com



#### 使用“源”来管理软件包

yum install 包的名字			//安装包
yum update				//更新
yum upgrade				//升级，包括升级系统，类windows update
yum remove				//删包
yum clean				//清理
yum list				//列出所有的包
yum list installed			//列出所有已经安装的包
yum search				//查找包

##### RPM包管理

rpm -qa					//查询系统中已经安装的软件
rpm -qf 文件名的绝对路径		//查询一个已经安装的文件属于哪个安装包
rpm -ql	软件名				//查询已经安装软件包都安装到何处
rpm -ivh rqm文件			//安装
rpm -Uvh rpm文件			//升级一个rpm文件
rpm -s 软件名				//删

##### bin文件安装

（1）设置文件可执行
（2）./文件名 直接运行

##### 源代码编译安装

（1）解压(tar)
（2）./configure [--prefiz=newpath](自己指定安装路径)
（3）make && make install（这一步要有root权限）



##### java环境配置

1. 对tar.gz文件，先解压，然后发现它只是jre 并不是jdk 这个文件就不必安装了
2. 在oracle的官方下载jdk 地址为：`https://www.oracle.com`

下载tar.gz的包

a.解压

b.`/etc/profile`中增加

`export JAVA_HOME=/你的java路径`
`export PATH=$PATH:$JAVA_HOME/bin`



1.安装
yum install -y httped

2.启动服务
service httpd start
systemctl start httpd

3.改端口
vim /etc/httpd/conf/httpd.conf
Listen 80

4.在本地访问
http://localhost
http://127.0.0.1
http://内网IP

5.找出web的根路径
DocumentRoot "/var/www/html"

6.发布静态页面
将静态文件放到/var/www/html目录下

7.关闭防火请,在局域网电脑上查看网页
service firewall stop
systemctl stop firewall
http://内网IP

9.发布虚拟目录
(1)在httpd.conf最后增加
	Alias /test "/var/www/test"
	<Directory "/var/www/test">
		options Indexes Multiviews
		Order allow.deny
		Allow from all
	</Directory>
(2)用root账号创建/var/www/test目录
(3)在/var/www/test目录下放html文件
(4)重启httpd
service httpd restart
(5)sudo setenforce 0;sudo getenforce;设置SELinux工作模式
(6)访问地址:http://ip/test

