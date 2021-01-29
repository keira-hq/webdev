#### 目标：在Linux服务器上安装Apache和FTP服务程序
#### 准备工作
- 云服务器操作系统：CentOS 8
- 本地PC上安装SSH客户端：SecureCRT、Xshell、Putty等任选其一进行安装（我用的是SecureCRT）[安装教程](https://mp.weixin.qq.com/s/42y7UvwzyjAZ7G7fWJoLeA)
    - 新建一个session 配置实例的密码 
    - 常见linux命令[菜鸟教程]（https://www.runoob.com/w3cnote/linux-common-command-2.html）
- 本地PC上安装WebStorm
*****

#### 安装Apache(在安装好的SecureCRT上在对应的文件内进行操作)
1. 安装

    yum install httpd 
 
2. 启动Apache

    systemctl start httpd

3. 设置开机启动

    systemctl enable httpd

4. 查看apache状态

    systemctl status httpd

5. 查看apache版本

    httpd -v

6. 查看防火墙状态，看看是否开启,如果没开启，跳过7-9步骤

    sudo systemctl status firewalld

7. 设置防火墙，允许http访问

    sudo firewall-cmd --permanent --zone=public --add-service=http

8.  设置防火墙，允许https访问

    sudo firewall-cmd --permanent --zone=public --add-service=https

9.  加载防火墙配置

    sudo firewall-cmd --reload

    通过运行以下命令，确保服务已正确授权

    sudo firewall-cmd --list-all | grep services

相关配置

    配置文件路径：/etc/httpd/conf/httpd.conf
    主目录：/var/www/html

*****

####  安装FTP
1. 安装

    yum install vsftpd
 
2. 启动Apache

    systemctl start vsftpd

3. 设置开机启动

    systemctl enable vsftpd --now

4. 查看ftp状态

    systemctl status vsftpd

5. 重启ftp服务

    systemctl restart vsftpd

6. 设置防火墙，允许ftp访问

    sudo firewall-cmd --permanent --add-port=20-21/tcp
    
    sudo firewall-cmd --permanent --add-port=30000-31000/tcp

    firewall-cmd --reload


7.  配置ftp用户

```
useradd -d /var/www/html -m newftpuser
sudo passwd newftpuser
echo "newftpuser" | sudo tee -a /etc/vsftpd/user_list
sudo chown -R newftpuser: /var/www/html
echo -e '#!/bin/sh\necho "This account is limited to FTP access only."' | sudo tee -a  /bin/ftponly
sudo chmod a+x /bin/ftponly
echo "/bin/ftponly" | sudo tee -a /etc/shells
```


ftp配置文件(/etc/vsftpd/vsftpd.conf) (去一个注释 加一段 其他不用动)
```
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
dirmessage_enable=YES
xferlog_enable=YES
connect_from_port_20=YES
xferlog_std_format=YES

chroot_local_user=YES（将文件内的注释去掉)


listen=NO
listen_ipv6=YES
pam_service_name=vsftpd
userlist_enable=YES

（最后加上这一段）
userlist_file=/etc/vsftpd/user_list
userlist_deny=NO
allow_writeable_chroot=YES
pasv_min_port=30000
pasv_max_port=31000

```

重启ftp服务   systemctl restart vsftpd

####  常见问题

查看selinux状态：sestatus

设置关闭selinux：setenforce 0

设置云服务商的安全组，将相应的端口开放

*****

####  webstorm设置ftp连接和自动同步的方法
常见问题：1 安全组打开端口80 21 30000/31000 2 “/”

[http://www.sunqizheng.com/blog/923.html](http://www.sunqizheng.com/blog/923.html)