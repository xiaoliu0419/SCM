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