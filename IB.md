# Infinband集群设置

<!-- TOC -->

- [Infinband集群设置](#infinband集群设置)
    - [IB本地化](#ib本地化)
        - [修改镜像](#修改镜像)
        - [镜像安装](#镜像安装)

<!-- /TOC -->

## IB本地化

### 修改镜像

修改镜像driver-one-shot中install-ib-drivers.sh内容

```
lspci | grep -qE '(Network|Infiniband) controller.*Mellanox.*ConnectX' || {
echo ======== No IB present, exit early =========
exit 1
}
echo "IB drivers skip"        #插入行
exit 0                        #插入行
```

修改后将此容器打包新镜像

```
sudo docker commit f915 sitonholy/drivers-410.73-noib:v0.12.1
```

将镜像上传至github

```
sudo docker pull sitonholy/drivers-410.73-noib:v0.12.1
```

此时，重启机器后IB驱动不会安装在容器中

### 镜像安装

在本机进入此目录,执行如下操作

```
cd /var/drivers/mellox/current
sudo ./uninstall.sh
sudo ./mlnxofedinstall
```

安装过程需要依赖，安装提示的包
```
sudo apt update
sudo apt install ...
```

等待其他包安装完成后，再重新执行命令

```
sudo ./mlnxofedinstall
```

完成过后固定IP地址

编辑文件`/etc/network/interfaces`

```
auto ib0
iface ib0 inet static
address 192.168.33.11
netmask 255.255.255.0
```

重启系统，完成安装