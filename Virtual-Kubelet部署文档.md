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
git clone https://github.com/CodePoetX/virtual-kubelet.git
cd $GOPATH/src/github.com/virtual-kubelet/virtual-kubelet/
go install
```

3. virtual-kubelet的可执行文件就会出现在`$GOPATH/bin/`当中
4. VK需要读取一些环境变量，用来注册自己到现有kubernetes集群中，因此我们需要设置一些环境变量，我们可以把需要的环境变量，写入一个脚本中，每次需要启动VK之前可以执行一下这个脚本，初始化环境变量，在脚本中写入如下内容.(注意：启动过程中，可能会提示缺少token和ca.crt文件，这两个文件是VK节点注册到kubernetes集群中需要的权限验证的两个文件，用户需要自己创建（如果安装了kubernetes dashboard 也可以用其保密字典，例如：
kubernetes-dashboard-admin-token-q7f2n）)
   
   4.1 `vi vk.sh` #写入内容如下
   
   4.2 source vk.sh

```
source ~/admin-openrc.sh    #openstack权限验证文件 可以通过dashboard生成
export OS_DOMAIN_NAME="default"
export KUBERNETES_SERVICE_HOST=XX.XX.XX.XX  #kubernetes master IP
export KUBERNETES_SERVICE_PORT=6443
export KUBELET_PORT=10250
$GOPATH/bin/virtual-kubelet --provider openstack    #启动命令
```

5. 启动VK

>
```
cd $GOPATH/bin/
./virtual-kubelet --provider openstack`
```
