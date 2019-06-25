# docker环境部署（基于阿里云的docker部署方法）
## 使用官方安装脚本自动安装 （仅适用于公网环境）
直接在linux系统中运行下列命令：

`curl -fsSL https://get.docker.com | bash -s docker --mirror Aliyun `

## Ubuntu 14.04或者16.04 (使用apt-get进行安装)
### step 1: 安装必要的一些系统工具
```
sudo apt-get update
sudo apt-get -y install apt-transport-https ca-certificates curl software-properties-common
```
### step 2: 安装GPG证书
```
curl -fsSL http://mirrors.aliyun.com/docker-ce/linux/ubuntu/gpg | sudo apt-key add -
```
### Step 3: 写入软件源信息
```
sudo add-apt-repository "deb [arch=amd64] http://mirrors.aliyun.com/docker-ce/linux/ubuntu $(lsb_release -cs) stable"
```
### Step 4: 更新并安装 Docker-CE
```
sudo apt-get -y update
sudo apt-get -y install docker-ce
```

## CentOS 7 (使用yum进行安装)
### step 1: 安装必要的一些系统工具
```
sudo yum install -y yum-utils device-mapper-persistent-data lvm2
```
### Step 2: 添加软件源信息
```
sudo yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```
### Step 3: 更新并安装 Docker-CE
```
sudo yum makecache fast
sudo yum -y install docker-ce
```
### Step 4: 开启Docker服务
```
sudo service docker start
```

## 安装校验
执行`docker version`命令
```
root@iZbp12adskpuoxodbkqzjfZ:$ docker version
Client:
 Version:      17.03.0-ce
 API version:  1.26
 Go version:   go1.7.5
 Git commit:   3a232c8
 Built:        Tue Feb 28 07:52:04 2017
 OS/Arch:      linux/amd64

Server:
 Version:      17.03.0-ce
 API version:  1.26 (minimum version 1.12)
 Go version:   go1.7.5
 Git commit:   3a232c8
 Built:        Tue Feb 28 07:52:04 2017
 OS/Arch:      linux/amd64
 Experimental: false
```

## 换源操作（使用阿里云源 拉取镜像加速）
```
sudo mkdir -p /etc/docker

sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://9w7g3j4y.mirror.aliyuncs.com"]
}
EOF

sudo systemctl daemon-reload

sudo systemctl restart docker
```