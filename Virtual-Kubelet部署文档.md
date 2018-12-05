# Virtual Kubelet部署文档（Zun版本）
## Golang环境部署
由于Virtual Kubelet是golang开发的，因此我们要通过源码部署VK（Virtual Kubelet），首先必须现在服务器上安装go语言环境。golang环境的部署安装我在同目录下面的文档有介绍，这里不在详述。

>[kubernetes的源码部署v1.12版本](https://github.com/CodePoetX/kubernetes-V1.12-kubernetes-/blob/master/kubernetes%E6%BA%90%E7%A0%81%E9%83%A8%E7%BD%B2.md)

## Virtual Kubelet的源码部署


1. 创建目录

> `mkdir -p $GOPATH/src/github.com/virtual-kubelet/`

2. 把vk的源代码代码从github上clone下来，然后放到这个目录下
```
cd $GOPATH/src/github.com/virtual-kubelet/
git clone https://github.com/kevin-zhaoshuai/virtual-kubelet.git
cd $GOPATH/src/github.com/virtual-kubelet/virtual-kubelet/
go install
```

3. virtual-kubelet的可执行文件就会出现在`$GOPATH/bin/`当中
4. 启动VK

>
```
cd $GOPATH/bin/
./virtual-kubelet --provider openstack`
```
