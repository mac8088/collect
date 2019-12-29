
## vsftp的安装与配置

### 安装

[root@node2 mac]# yum install -y vsftpd
[root@node2 mac]# rpm -qa|grep vsftp
vsftpd-3.0.2-25.el7.x86_64
[root@node2 mac]# 

[root@node2 mac]# cd /etc/vsftpd/
[root@node2 vsftpd]# ls
ftpusers  user_list  vsftpd.conf  vsftpd_conf_migrate.sh

### 匿名设置

将默认目录赋予用户ftp权限以便于可以上传文件

	[root@node2 ~]# ls /var/ftp/pub/ -la
	total 0
	drwxr-xr-x. 2 root root  6 Oct 31  2018 .
	drwxr-xr-x. 3 root root 17 Aug  5 11:53 ..
	[root@node2 ~]# 
	[root@node2 ~]# chown -R ftp.users /var/ftp/pub/
	[root@node2 ~]# 
	[root@node2 ~]# ls /var/ftp/pub/ -la
	total 0
	drwxr-xr-x. 2 ftp  users  6 Oct 31  2018 .
	drwxr-xr-x. 3 root root  17 Aug  5 11:53 ..
	[root@node2 ~]# 


编辑之前：

	[root@node2 ~]# vi /etc/vsftpd/vsftpd.conf 
	# Example config file /etc/vsftpd/vsftpd.conf
	#
	# The default compiled in settings are fairly paranoid. This sample file
	# loosens things up a bit, to make the ftp daemon more usable.
	# Please see vsftpd.conf.5 for all compiled in defaults.
	#
	# READ THIS: This example file is NOT an exhaustive list of vsftpd options.
	# Please read the vsftpd.conf.5 manual page to get a full idea of vsftpd's
	# capabilities.
	#
	# Allow anonymous FTP? (Beware - allowed by default if you comment this out).
	anonymous_enable=YES
	#
	# Uncomment this to allow local users to log in.
	# When SELinux is enforcing check for SE bool ftp_home_dir
	local_enable=YES
	#
	# Uncomment this to enable any form of FTP write command.
	write_enable=YES
	#
	# Default umask for local users is 077. You may wish to change this to 022,
	# if your users expect that (022 is used by most other ftpd's)
	local_umask=022
	#
	# Uncomment this to allow the anonymous FTP user to upload files. This only
	# has an effect if the above global write enable is activated. Also, you will
	# obviously need to create a directory writable by the FTP user.
	# When SELinux is enforcing check for SE bool allow_ftpd_anon_write, allow_ftpd_full_access
	#anon_upload_enable=YES
	#
	# Uncomment this if you want the anonymous FTP user to be able to create
	# new directories.
	#anon_mkdir_write_enable=YES
	#
	# Activate directory messages - messages given to remote users when they
	# go into a certain directory.
	dirmessage_enable=YES
	#
	# Activate logging of uploads/downloads.
	xferlog_enable=YES
	#
	# Make sure PORT transfer connections originate from port 20 (ftp-data).
	connect_from_port_20=YES
	#
	# If you want, you can arrange for uploaded anonymous files to be owned by
	# a different user. Note! Using "root" for uploaded files is not
	# recommended!
	#chown_uploads=YES
	#chown_username=whoever
	#
	# You may override where the log file goes if you like. The default is shown
	# below.
	#xferlog_file=/var/log/xferlog
	#
	# If you want, you can have your log file in standard ftpd xferlog format.
	# Note that the default log file location is /var/log/xferlog in this case.
	xferlog_std_format=YES
	#
	# You may change the default value for timing out an idle session.
	#idle_session_timeout=600
	#
	# You may change the default value for timing out a data connection.
	#data_connection_timeout=120
	#
	# It is recommended that you define on your system a unique user which the
	# ftp server can use as a totally isolated and unprivileged user.
	#nopriv_user=ftpsecure
	#
	# Enable this and the server will recognise asynchronous ABOR requests. Not
	[root@node2 ~]# 


取消配置文件中的注释并显示有效的行

	[root@node2 ~]# grep -v ^# /etc/vsftpd/vsftpd.conf 
	anonymous_enable=YES
	local_enable=YES
	write_enable=YES
	local_umask=022
	dirmessage_enable=YES
	xferlog_enable=YES
	connect_from_port_20=YES
	xferlog_std_format=YES
	listen=NO
	listen_ipv6=YES
	pam_service_name=vsftpd
	userlist_enable=YES
	tcp_wrappers=YES
	[root@node2 ~]# 

配置修改后，重新过滤显示：

	[root@node2 ~]# grep -v ^# /etc/vsftpd/vsftpd.conf 
	anonymous_enable=YES
	local_enable=YES
	write_enable=YES
	local_umask=022
	anon_upload_enable=YES
	dirmessage_enable=YES
	xferlog_enable=YES
	connect_from_port_20=YES
	xferlog_std_format=YES
	listen=YES
	listen_ipv6=NO

	pam_service_name=vsftpd
	userlist_enable=YES
	tcp_wrappers=YES
	[root@node2 ~]# 
	
	
### 启动FTP

	[root@node2 ~]# systemctl start vsftpd
	[root@node2 ~]# 
	[root@node2 ~]# ps -ef | grep vsftpd

	root       7253      1  0 12:12 ?        00:00:00 /usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf
	root       7255   7126  0 12:12 pts/0    00:00:00 grep --color=auto vsftpd
	[root@node2 ~]# 
	[root@node2 ~]# 

### 开机启动

[root@node2 mac]# systemctl enable vsftpd && systemctl start vsftpd
Created symlink from /etc/systemd/system/multi-user.target.wants/vsftpd.service to /usr/lib/systemd/system/vsftpd.service.
[root@node2 mac]# 
