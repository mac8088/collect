
##

### 公共命令

	touch file

### CentOS

#### 安装Docker


Docker local registry

	$ docker run -d -p 5000:5000 --restart=always --name registry registry:2

	
Install Compose on Linux systems

	$ sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
	
	$ sudo chmod +x /usr/local/bin/docker-compose


	$ docker-compose version
		docker-compose version 1.23.2, build 1110ad01
		docker-py version: 3.6.0
		CPython version: 3.6.7
		OpenSSL version: OpenSSL 1.1.0f  25 May 2017

Install Docker machine on linux

	$ base=https://github.com/docker/machine/releases/download/v0.16.0 &&
	  curl -L $base/docker-machine-$(uname -s)-$(uname -m) >/tmp/docker-machine &&
	  sudo install /tmp/docker-machine /usr/local/bin/docker-machine


### Ubuntu

查看Ubuntu的版本：

	mac@ubuntu:~$ cat /etc/lsb-release 
	DISTRIB_ID=Ubuntu
	DISTRIB_RELEASE=18.04
	DISTRIB_CODENAME=bionic
	DISTRIB_DESCRIPTION="Ubuntu 18.04.1 LTS"
	mac@ubuntu:~$ 

查看Ubuntu虚拟机IP地址：

	mac@ubuntu:~$ ip addr
	1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
	    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
	    inet 127.0.0.1/8 scope host lo
	       valid_lft forever preferred_lft forever
	    inet6 ::1/128 scope host 
	       valid_lft forever preferred_lft forever
	2: ens33: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
	    link/ether 00:0c:29:80:82:97 brd ff:ff:ff:ff:ff:ff
	    inet 192.168.80.133/24 brd 192.168.80.255 scope global dynamic noprefixroute ens33
	       valid_lft 1538sec preferred_lft 1538sec
	    inet6 fe80::3a8:f147:96d3:7b84/64 scope link noprefixroute 
	       valid_lft forever preferred_lft forever
	mac@ubuntu:~$ 

或者使用ifconfig：

	mac@ubuntu:~$ ifconfig
	ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
	        inet 192.168.80.133  netmask 255.255.255.0  broadcast 192.168.80.255
	        inet6 fe80::3a8:f147:96d3:7b84  prefixlen 64  scopeid 0x20<link>
	        ether 00:0c:29:80:82:97  txqueuelen 1000  (Ethernet)
	        RX packets 432572  bytes 445170761 (445.1 MB)
	        RX errors 0  dropped 0  overruns 0  frame 0
	        TX packets 228421  bytes 14745664 (14.7 MB)
	        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
	
	lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
	        inet 127.0.0.1  netmask 255.0.0.0
	        inet6 ::1  prefixlen 128  scopeid 0x10<host>
	        loop  txqueuelen 1000  (Local Loopback)
	        RX packets 567  bytes 47107 (47.1 KB)
	        RX errors 0  dropped 0  overruns 0  frame 0
	        TX packets 567  bytes 47107 (47.1 KB)
	        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
	
	mac@ubuntu:~$ 


如果不存在ifconfig，需要安装：

	mac@ubuntu:~$ sudo apt install net-tools
	[sudo] password for mac: 
	Reading package lists... Done
	Building dependency tree       
	Reading state information... Done
	net-tools is already the newest version (1.60+git20161116.90da8a0-1ubuntu1).
	0 upgraded, 0 newly installed, 0 to remove and 284 not upgraded.
	mac@ubuntu:~$ 


检查SSH：

	mac@ubuntu:~$ ssh localhost
	ssh: connect to host localhost port 22: Connection refused
	mac@ubuntu:~$ 
	mac@ubuntu:~$ netstat -ntlp | grep 22
	Command 'netstat' not found, but can be installed with:
	sudo apt install net-tools
	mac@ubuntu:~$ 


关闭防火墙：

	mac@ubuntu:~$ sudo ufw disable


打开SSH服务，开启22端口，执行以下命令：

	sudo apt-get install openssh-server
	sudo apt-get install ufw (optional)
	sudo ufw enable (optional)
	sudo ufw allow 22

重启ssh服务：  

	service sshd restart
	或者：
	sudo /etc/init.d/ssh restart

查看22端口状态：

	mac@ubuntu:~$ netstat -tnl 
	Active Internet connections (only servers)
	Proto Recv-Q Send-Q Local Address           Foreign Address         State      
	tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN     
	tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN     
	tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN     
	tcp6       0      0 :::22                   :::*                    LISTEN     
	tcp6       0      0 ::1:631                 :::*                    LISTEN     
	mac@ubuntu:~$ 


- 查看已经连接的服务端口（ESTABLISHED): netstat -a　
- 查看所有的服务端口（LISTEN，ESTABLISHED） netstat -ap

查看哪些进程打开了指定端口：

使用 netstat -nap  |grep port 最后一列是进程ID（此方法对于守护进程作用不大）

使用aptitude安装应用

	mac@ubuntu:~$ sudo apt-get install aptitude
	mac@ubuntu:~$ sudo show vim
	mac@ubuntu:~$ sudo search vim
	mac@ubuntu:~$ sudo install vim


#### 在Ubuntu中安装Docker

##### 安装之前的检查

内核检查

	mac@ubuntu:~$ uname -a
	Linux ubuntu 4.15.0-29-generic #31-Ubuntu SMP Tue Jul 17 15:39:52 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
	mac@ubuntu:~$ 

检查设备映射

	mac@ubuntu:~$ ls -l /sys/class/misc/device-mapper
	lrwxrwxrwx 1 root root 0 Jan 18 14:54 /sys/class/misc/device-mapper -> ../../devices/virtual/misc/device-mapper
	mac@ubuntu:~$














