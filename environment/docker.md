> 这里以Ubuntu 22.04 来举例
## docker安装
教程地址：https://docs.docker.com/engine/install/ubuntu/
```shell
# 删除旧版本
sudo apt-get remove docker docker-engine docker.io containerd runc
# 安装依赖
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
# 添加GPG秘钥
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
# 安装
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

# 服务启动
sudo service docker start
# 开机自启
sudo systemctl enable docker.service
```


## nvidia支持
官方文件地址: https://github.com/NVIDIA/nvidia-docker
```shell
##首先要确保已经安装了nvidia driver
# 2. 添加源
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list

# 2. 安装并重启
sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit
sudo systemctl restart docker
```

## 使用

> 主要核心的就是需要加上 `--gpus all` 才可以支持显卡

```shell
sudo docker run -itd --gpus all nvidia/cuda:11.0.3-base-ubuntu20.04
# 进入容器后输入nvidia-smi 就可以看到显卡信息了
```

一些常用库的开源镜像地址
```shell
# pytorch
docker pull pytorch/pytorch:1.9.1-cuda11.1-cudnn8-runtime
```