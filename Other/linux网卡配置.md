#克隆后用ifconfig出现link encap local loopback

![](./_image/2018-01-23-16-47-50.jpg)

先检查 虚拟网络设置 无误
再检查发现克隆的虚拟机和克隆后虚拟机物理网址冲突
![](./_image/2018-01-23-11-03-14.jpg)
启动网卡eth1
```
# ifconfig eth1 up
```
![](./_image/2018-01-23-11-04-59.jpg)
切换到网络配置文件夹， 新建eth1
```
# cd /etc/sysconfig/network-scripts
# mv ifcfg-eth0 ifcfg-eth1
```
修改 ifcfg-eth1配置信息
![](./_image/2018-01-23-11-48-01.jpg)
重启网络服务
```
# service network restart
```
使用命令ifconfig再次查看，就已经配置好
