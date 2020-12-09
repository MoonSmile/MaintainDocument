
## Server端
NFS默认是已经安装的，所以只需启动服务即可
### 关闭防火墙以免用户连接被防火墙拒绝
	setenforce 0
	systemctl stop firewalld.service
	systemctl disable firewalld.service

### 编辑exports文件，添加从机
    vim /etc/exports
    /home/nfs/ 192.168.1.0/24(rw,sync,fsid=0)

### 启用nfs服务并设置开机自启动
	systemctl start  rpcbind.service
	systemctl start nfs-server.service
	systemctl enable rpcbind.service
	systemctl enable nfs-server.service

### 检查服务
    rpcinfo -p
	exportfs
	
## 客户端
	mkdir /app/ga/gaFile
	mount nfs-server-ip:/app/ga/gaFile /app/ga/gaFile  #nfs-server-ip为nfs服务器的IP地址
	df -h #查看挂载是否成功
