# Docker安装教程

## 在Ubuntu主机安装Docker\
    ```
    curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun
    ```

## docker-compose安装
    ```
    # 将docker-compose下载到``
    sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    # 赋予docker-compose执行权限
    sudo chmod +x /usr/local/bin/docker-compose
    ```