# TroubleShooting

编写此文档的意义在于排除搭建过程中遇到的各类问题
编写的内容不会很完善，有任何问题请联系Sitonholy

#### K8s无法启动

1. 请检查硬件配置是否符合标准[硬件选用](./README#硬件选用)

2. 如果部署成功过，因为配置原因无法重启K8s服务的话，则在dev-box尝试清除K8s集群环境

```
cd /pai
./paictl cluster k8s-clean -p ~/pai-config -f
```

#### 驱动容器无法启动

1. 在k8s-dashboard中查看显卡驱动报错原因

2. 尝试删除驱动重新部署

```
./paictl service delete -n drivers
```

#### 新建集群无法找到显卡

请参考[部署节点](./README.md#部署节点)

#### pylon报错

查询某一个节点的docker，看是否有某一个docker占用了Pylon所用的端口号

#### grafana抓不到数据

先看一下prometheus主机时间和客户机是否一致，不一致则调整时间为一致

#### 自建容器无法打开web ssh服务

在容器中安装openssh-server和curl服务，将容器生成新镜像
用新镜像重启启动任务即可打开

#### 我应当如何使用命令行连接到容器中

对于我们打包的镜像，您可以使用

`ssh -p {端口号} {容器所在节点IP}`

进行登录


如果您需要自己打包镜像

需要提前在容器中安装`openssh-server `

然后打开root登录权限，并设置root密码

打开ssh配置文件 `/etc/ssh/sshd_config`   

修改`PermitRootLogin yes`

然后重启ssh服务

`service ssh restart`

就可以连接了

#### 文件管理中的文件在容器的哪里？

在容器中，您需要切换到路径`/root/data`下进行工作

其他目录不会被映射到主机的NFS空间中


#### 我应当如何上传或下载私有镜像

当您在容器中做修改，您可以先登录到对应节点的主机上查找容器

`docker ps|grep {任务名称}`

找到容器后进入容器

`docker exec -it {任务对应容器id} bash`

安装ssh,curl服务

`apt install openssh-server curl -y`

设置root密码

`passwd root`

修改配置文件`/etc/ssh/sshd_config`

将此行修改为`PermitRootLogin yes`

重启ssh服务`service ssh restart`
