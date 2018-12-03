# **kubernetes的源码部署v1.12版本**

## golang v1.10.2的安装
--- 

由于kubernetes是golang语言开发的，因此为了通过源码部署kubernetes，我们必须首先部署golang语言环境。kubernetes的版本对于语言支持有要求，我们可以具体查看此链接或者下表：

[Development Guide](https://github.com/kubernetes/community/blob/master/contributors/devel/development.md)

Kubernetes|requires Go
:--:|:--:
1.0 - 1.2|1.4.2
1.3, 1.4|1.6
1.5, 1.6|1.7 - 1.7.5
1.7|1.8.1
1.8|1.8.3
1.9|1.9.1
1.10|1.9.1
1.11+|1.10.2

由于我们想基于最新版本的kubernetes源码进行开发，因此我们这里需要部署golang V1.10.2的开发环境。
### 部署环境
操作系统：centos7
### 步骤
1. 首先去下载golang V1.10.2的安装包。 ([go1.10.2.linux-amd64.tar.gz](https://studygolang.com/dl/golang/go1.10.2.linux-amd64.tar.gz))（centos7命令：
   1. `yum update -y && yum install wget git -y`
   2.  `wget https://studygolang.com/dl/golang/go1.10.2.linux-amd64.tar.gz`
   ）
2. 在服务器上解压此压缩包到 /usr/local/ 文件夹下面.(centos7命令：
   1. `tar zxvf go1.10.2.linux-amd64.tar.gz -C /usr/local/` 
   2. 编辑文件 `vi /root/.bash_profile`，在文件的最后添加如下语句：
```shell
export PATH
export GOROOT=/usr/local/go 
export GOBIN=$GOROOT/bin
export GOPKG=$GOROOT/pkg/tool/linux_amd64 
export GOARCH=amd64
export GOOS=linux
export GOPATH=/go
export PATH=$PATH:$GOBIN:$GOPKG:$GOPATH/bin:/go/src/k8s.io/kubernetes/_output/local/go/bin/
```
3. 此时golang的环境就部署完成了，我们可以执行 `go version` 命令查看。golang的工作目录是：`/go/`

## kubernetes V1.12源码编译
---
我们部署好golang环境后，就可以从github上拉取kubernetes源码，进行编译了。github上kubernetes主页通过下面的命令对源码进行拉取并自动编译。
> 
```
$ go get -d k8s.io/kubernetes
$ cd $GOPATH/src/k8s.io/kubernetes
$ make
```
但是我在我本地环境执行上述命令 `go get -d k8s.io/kubernetes`就卡住不动了，后来通过查错发现是代码通过上面的命令并不能拉取到代码，因此我改用手动的办法，下面介绍详细步骤。

### 步骤
1. 在 `$GOPATH` 路径下新建源码文件夹，代码如下：

`mkdir -p $GOPATH/src/k8s.io`

`cd $GOPATH/src/k8s.io`

`git clone -b release-1.12 https://github.com/kubernetes/kubernetes.git`

`cd $GOPATH/src/k8s.io/kubernetes`

`make`

2. 此时我们稍等片刻，make会自动去拉取安装过程中需要的一些golang包，其中可能部分包不能拉取到，我们需要去网上找到相应缺少的包，并且导入到报错提示的路径下面，然后再次执行 `make` 指令。

3. 执行成功后，生成的可执行文件会在下面文件夹自动生成：

`cd $GOPATH/src/k8s.io/kubernetes/_output/local/bin/linux/amd64`

4. 最后将kubernetes的amd64目录下面所有编译之后的代码全部复制出来，最后进行安装。









