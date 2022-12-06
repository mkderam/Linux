## kubernetes简介
:::danger
Kubernetes 是一个开源的容器编排引擎和容器集群管理工具，用来对容器化应用进行自动化部署、扩缩和管理。
Kubernetes 这个名字源于希腊语，意思为"舵手"或"飞行员",k8s是因为kubernetes这个单词k到s之间有8个字母。google在2014年开源了kubernetes项目。
优势：kubernetes是建立在Google 大规模运行生成工作负载十几年的基础上，结合了社区中最优秀的想法和实践。它之所以能迅速流行起来，是因为它许多功能高度契合互联网运维大厂和运维需求
kubernetes可以提供：
服务发现和负载均衡
kubernetes可以使用DNS名称或者自己的IP来暴露容器。如果进入容器的流量很大kubernetes可以负载均衡并分配网络流量，从而使部署稳定
存储编排
kubernetes允许你自动关注你选择的存储系统，例如本地存储，公共云提供商等。
自动部署和回滚
你可以使用Kubernetes描述已部署容器所需状态，它可以以受控的速率将实际状态更改为期望状态。例如，你可以自动化Kubernetes来为你部署创建新容器，删除现有容器并将它们的所有资源用于新容器。也可以是方便的实现金丝雀部署
自动完成装箱计算
你为kubernetes提供许多节点组成的集群，在这个集群上运行容器化的任务，你告诉kubernetes每个容器多少CPU和内存(RAM)。kuberbnetes可以将这些容器按实际导读到你的节点上，以最佳方式利用你的资源
自我修复
kuberntes将重新齐东东失败的容器，替换容器，杀死不响应用户自定义的运行状况检查容器，并且在准备好服务之前不讲其通告给客户端。
秘钥与配置管理
Kubernetes允许你存储和管理敏感信息，例如密码、OAuth令牌和ssh秘钥。你可以在不重建容器镜像的情况下部署和更新秘钥和应用程序配置，也无需在堆栈中暴露秘钥。

云原生
2015年有Google、Redhat等大型云厂商以及一些开源公司牵头成立了Cloud Native Computing Foundation(云原生计算基金会)。
云原生计算基金会(CNCF) 致力于培育和维护一个厂商中立的开源生态系统，来推广云原生技术。
云原生的概念从此广泛传播
云原生定义
Kubernetes是CNCF托管得第一个开源项目。因此现在提到云原生，往往我们都把它与KUbernetes联系起来。
通俗解释：
使用Java，Go PHP Python等语言开发得用用我们称之为原生应用，在设计和开发这些应用时，是他们能够运行在基础设施(或Kubernetes)上，从而使应用具备弹性扩展得能力，我们称之位原生应用。我们可以将云原生理解位以容器技术位载体，基于微服务架构思想得一套技术体系和方法论。
云原生官方定义：
云原生技术有立域组织在共有云、私有云和混合云等新型动态环境中，构建和运行可扩展得应用。云原生代表技术包括容器、服务网格、微服务、不可变基础设施和声明式API
这些技术能够构建容错性好、易于管理便于观察和松耦合系统。结合可靠得自动收段，云原生技术使用工程师能够轻松地对系统做出频繁和可预测得重大变更。
简单来讲：就是能够减轻运维和实施得工作量，提高自动化程度
微服务：Spring cloud和kubernetes有很多功能是重合得。例如：服务注册和发现\API网关、负载均衡、配置管理
spring cloud 只能用于java开发。kubernetes是语言无关得，可以用于各种语言
:::
## kubernetes架构
:::danger
一个kubernetes集群至少包含一个控制平面，以及一个或者多个工作节点。
控制平面：控制平面负责管理工作节点和维护集群状态。所有任务分配都来自控制平面
kube-apiserver:
如果需要与kubernetes集群进行交互，就需要通过API.
apiserver是kubernetes控制平面的前端，用于处理内部和外部请求。
kube-scheduler:
集权状况是否良好？如果需要创建新的容器，要将它们放在那里？这些是调度程序需要关注的问题
scheduler 调度程序会考虑容器集的资源需求(例如CPU或内存)以及集群的运行状况。随后，它会将容器安排到适当的计算机节点
kube-controller-manager:
控制器负责实际运行集群，controller-manager控制器管理则时间多个控制器空格合而为一，降低复杂度。
控制器包含这些控制器：
节点控制器(Node controller):负责在节点出现故障时进行通知和响应
任务控制器（job controller）检测代表一项任务的Job对象，然后创建Pods来运行这些任务直至完成
端点控制器(Endpoints Controller):填充端点（Endpoints）对象(即加入service与Pod)
服务账户和令牌控制器（server Account & Token controllers）:为新的命名空间创建默认账户和API访问令牌
etcd:
etcd是一个键值对数据库，用于存储配置数据和集群状态信息
工作节点：工作节点负责有控制平面分配请求任务，运行实际的应用和工作负载
Node组件负责维护运行的pod并提供Kubernetes运行环境
kubelet:
kubelete会在句群中每个节点上运行。它保证容器都运行在Pod中
当控制平面需要在节点中执行某个操作时，kubelet就会执行该操作
kube-proxy:
实际群中么个节点运行的网络代理，是实现kubernetes服务概念的一部分
维护节点网络规则和转发流量，实现从集群内部的网络与pod进行网络通信
container runtime:
容器运行环境是负责运行容器的软件
kubenetes支持许多容器运行环境，例如containerd,docker或者其他实行了Kubernetes CRI(容器云环境接口)的容器

控制平面还包含了一个可选组件云平台控制器（Clouid controller Manager）允许你将集群中连接到云提供商的API之上，并将与改平台交互的组件同你的集群交互组件分类开来。
自己环境运行kubernetes,或者本地学习将不需要
:::
## 常用命令缩写
| 名称 | 缩写 | kind |
| --- | --- | --- |
| namespaces | ns | Namespace |
| nodes | no | Node |
| pods | po | Pod |
| services | svc | Service |
| deploymnets | deploy | Deployment |
| replicasets | rs | ReplicaSet |
| statefulsets | sts | StatefulSet |

## 安装minikube
:::info
minikube 是一个可以运行在本地单机版的kubernetes,方便我们学习kubernetes和调试程序
安装minikube使用需要使用虚拟机或docker.推荐使用docker
:::

- 运行环境
   - 至少两核
   - 内存不低于2GB
   - 磁盘不低于20GB
   - 联网环境（或docker）
```
启动minikube 需要两个参数
--image-mirror-country='cn'
设置使用国能阿里云镜像
--container-runtime=containerd
设置容器运行时为containerd
```
> minikube默认安装kubernetes v1.25.0，需要将容器运行时设置为containerd
> 运行v1.24.0及之后版本，都需要此设置。如果不设置会报错

## 使用k3s快速搭建集群
## 为什么使用k3s
:::info
k3s是一个轻量级的，完全兼容kubernetes发行版本。
:::

- 运行环境
   - 最低运行要求
      - 内存512/cpu1
      - k3s版本：v1.25.0+k3s1
      - 进群规划
| 主机名 | ip地址 | 配置 | 系统 | 网络 |
| --- | --- | --- | --- | --- |
| k8s-master | 192.168.14.109 | 内存：2G
CPU：2核
硬盘：20GB | centos7.9.2009 | 互联网：net网络
内部网络：Host-only |
| k8s-worker1 | 192.168.14.111 |  |  |  |
| k8s-worker2 | 192.168.14.112 |  |  |  |

```
准备
yum install -y container-selinux
yum install -y https://rpm.rancher.io/k3s/stable/common/centos/7/noarch/k3s-selinux-0.4-1.el7.noarch.rpm
systemctl stop 
systemctl disable firewalld
master
下载insert.sh  k3s  k3s-airgap-images-amd64.tar
wget https://rancher-mirror.oss-cn-beijing.aliyuncs.com/k3s/k3s-install.sh
wget 
mv k3s /usr/local/bin
chmod +x /usr/local/bin/k3s
mkdir -p /var/lib/rancher/k3s/agent/images/
chmood +x install.sh
cat  /var/lib/rancher/k3s/server/node-token

work1

INSTALL_K3S_SKIP_DOWNLOAD=true \
K3S_URL=https://192.168.14.109:6443 \
K3S_TOKEN=K1037b3ec39269245af17c6a3c54ae4952be8d227c33efc450b92ac0cd183366ba0::server:d0bbf455f5f1fa9fd94a804baff41ff6 \
./k3s-install.sh

work2
INSTALL_K3S_SKIP_DOWNLOAD=true \
K3S_URL=https://192.168.14.109:6443 \
K3S_TOKEN=K1037b3ec39269245af17c6a3c54ae4952be8d227c33efc450b92ac0cd183366ba0::server:d0bbf455f5f1fa9fd94a804baff41ff6 \
./k3s-install.sh

镜像加速
修改containerd镜像
/etc/containerd/config.toml
k3s中配置镜像仓库
k3s 会自动生成containerd的配置文件/var/lib/rancher/k3s/agent/etc/containerd/config.toml 不要直接修改这个文件。k3s重启之后会丢失
为了简化配置，k3s通过/etc/rancher/k3s/registries.yaml 文件来配置镜像仓库，k3s会在启动时检查这个文件是否存在
我们需要在每个节点是新建 /etc/rancher/k3s/registries.yaml 文件配置如下：
vim /etc/rancher/k3s/registries.yaml
mirrors:
  docker.io:
    endpoint:
      - "https://fsp2sfpr.mirror.aliyuncs.com"

systemctl  restart k3s
systemctl  restart k3s-agent
```
## Pod(容器集)
:::info
Pod是包含一个或多个容器的容器组，是kubernetes中创建和管理的最小对象。
pod特点：
Pod是kubernetes中最小的调度单位(原子单元)，kubernetes直接管理Pod而不是容器。
同一个pod中的容器总是会被自动安排到同一节点(物理机或者虚拟机)是上，并且一起调度
pod可以理解为运行特定应用的"逻辑主机"，这些容器共享存储、网络和配置声明（如资源限制）
每个Pod有唯一的IP地址。ip地址分配给pod,在同一个Pod内，所有容器共享一个IP地址和端口空间，pod内的容器可以使用localhost互相通信。
:::
```shell
获取node节点信息
kubectl  get node
创建pod
kubectl run mynginx --image=nginx:1.22
获取pod状态
kubectl get pod
pod日志
kubectl  logs  -f mynginx
获取pod详细信息
kubectl describe pod mynginx
获取状态详细信息
kubectl get pod -owide
#进入pod
kubectl exec -it mynginx  -- /bin/bash
#退出交互直接删除pod
kubectl exec -it mynginx  -- /bin/bash  --rm
#删除容器
kubectl delete pod  '容器'
查看Pod所有属性
kubectl get pod -A
#查看指定命名空间的pod 如果不指定默认查看default
kubectl get pod -n=devlop
#查看容器带有的标签
kubectl get pod --show-labels
#使用标签顾虑查看pod,如果有多个标签使用逗号分隔他们之间是and关系
kubectl get pod -l "app=nginx"
```
## Deployment(部署)与ReplicaSet(副本集)
:::info
deployment 是对ReplicaSet和Pod更高级的抽象
它使Pod拥有多副本，自愈，扩缩容，滚动升级等能力

ReplicaSet(副本集)是一个Pod的集合
它可以设置运行Pod的数量，确保任何时间都有自定数量的pod副本在运行。通常我们不直接使用Replicaset.而是在Deployment中声明。
:::
```shell
创建deployment并制定副本集
kubectl create deployment nginx-deploy --image=nginx:1.22 --replicas=3
获取deployment
kubectl get deploy
获取replicaset
kubectl get replicaSet
#扩容副本集
kubectl scale deploy nginx-deploy --replicas=3
```
:::info
自动缩放
自动缩放通过增加和减少副本的数量，以保持所有pod的平均cpu利用率不超过75%。自动伸缩需要pod的资源限制。同时使用metrics Service 服务(k3s默认安装)
本例仅用来说明kubectl autoscale命令的使用，完整实例参考：HPA演示
:::
```shell
kubectl get deploy -owide 
kubectl set image deploy/nginx-deploy  nginx=nginx:1.23
#查看更新版本
kubectl rollout  history deploy/nginx-deploy
#查看第一跟新的详细信息
kubectl rollout  history deploy/nginx-deploy --revision=1
#回滚到第一次跟新
kubectl rollout  undo deploy/nginx-deploy  --to-revision=1 

#查看全部信息
kubectl get all 

```
## Service(服务)
:::info
Service 将运行一组Pods上的应用程序公开为网络的抽象方法。
service为一组pod提供相同DNS名，并且在他们之间进行负载均衡
kubernetes 为pod提供分配ip地址，但ip地址可能会发生变化
集群内部的容器可以同伙service名称访问服务，而不需要担心pod的ip发生变化


kubernetes Service定义了这样一种抽象：
逻辑上的一组可以替换的Pod,通常称为微服务
Service对应的Pod集合通常是通过选择来确定的
举个例子：在一个Service中运行了3个nginx副本。这些副本是可替换的，我们不需关系调用了那个nginx,也不需要关注Pod的运行状态，只需要调用这个服务就可以了

servicetype 取值
ClusterIP：将服务公开在集群内部。kubernetes会给服务分配一个集群内部的IP,集群内的所有主机都可以通过这个Cluster-ip访问服务、集群内部的pod可以通过Service名称访问服务
Nodeport:通过每个几点的主机IP和静态端口(nodeport) 暴露服务。集群的外部主机可以使用节点ip和nodePort范问服务
ExternalName:将集群外部的网络引入进群内部
loadBalancer:使用云提供商的负载均衡器向外部暴露服务。
:::
```shell
#将一个servue 暴露端口
kubectl expose deploy/nginx-deploy  --name=nginx-service --port=8080 --target-port=80
#列出一个service的详细信息
 kubectl describe service nginx-service
 kubectl describe svc/my-service
#将pod
kubectl expose deploy/nginx-deploy  --name=nginx-outside --type=NodePort --port=8081  --target-port=80
kubectl get service

```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/34405776/1670242360511-c5a4069b-7a81-4749-92b6-00952106f8ca.png#averageHue=%23fbfbfa&clientId=ub1530f7e-f6f6-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=454&id=uce105c5b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=454&originWidth=536&originalType=binary&ratio=1&rotation=0&showTitle=false&size=32200&status=done&style=none&taskId=u5a59b484-bf4d-425b-b1e7-868640fe130&title=&width=536)
## Namespace(命名空间)
:::info
命名空间(Namespace)是一种资源隔离机制，将同一集群中的资源划分为相互隔离的组。
名空可以在多个用户之间划分集群资源(通过资源配置)
例如我们可以设置开发，测试，生产多个命名空间
同一命名空间内的资源名称要唯一，单跨命名空间是没有这个要求
命名空间作用域仅针对带有名字空间的对象，例如：Deployment,Service等
这种作用域对集群访问的对象不适用，例如：storageclass,node,persistentVolume


kubernetes 会创建四个初始命名空间：
default 默认命名空间。不可删除，未指定命名空间都会分配到defalut中
kube-system  Kubernetes系统对象(控制平面和Node组件)所使用的的命名空间
kube-public 自动创建的公共命名空间，所有用户(包括未经身份验证的用户)都可以读取它。通常我们约定，将整个集群中公用可见和可读的资源放在这个空间中。
kube-node-less  租约(Lease) 对象使用的命名空间。每个节点都有一个关联lease对象，lease是一种轻量级资源。lease对象通过发送心跳，检测集群中的每个节点是否发生故障。

使用kubectl get lease -A    #查看lease对象
:::
```shell
kubectl get Namespaces

kube get lese -A

 kubectl create ns devlop    #创建一个名为devlop的命名空间(namespace可以缩写为ns)

kubectl run nginx  --image=nginx:1.22  -n=develop
#更改查看默认命名空间的查看格式
kubectl config  set-context  $(kubectl config current-context) --namespase=devlop
删除命名空间
kubectl delete ns develop

如果无法删除，需要删除资源后再删除命名空间
```
## 声明式对象配置
:::info
kubernetes  管理对象
命令行式管理
介绍：使用kubectl命令穿件和管理kubernetes对象
优点：简单，快速，高效
缺点：功能有限，不适合复杂场景，操作不容易追溯，多用于开发和调试
声明式：
介绍：kubernetes使用yaml文件描述kubernetes对象
缺点：学习难度大，配置麻烦
优点：适合操作复杂的对象，多用于生产，操作留痕
:::

- YAML规范
   - 缩进代表上下级关系
   - 缩进不允许使用Tab键。只允许使用空格，通常缩进2个空格
   - ：键值对，后面必须有空格
   - [] 数组
   - #注释
   - | 多行文本块
   - ----表示文档的开始，多用于分割多个资源对象
配置对象在创建的kubernetes对象对用的yaml中需要配置的字段如下：

- apiVersion  - Kubernetes API的版本
- kind -  对象类别，例如Pod、Deployment、Service、ReplicaSet等
- metadata-描述对象的元数据，包括一个name字符串，Uid和可选的namespase
- spec-对象的配置

掌握程度

- 不要求自己会写
- 找模板
- 能看懂
- 会修改
- 能排错
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.22
    ports:
    - containerPort: 80


#使用配置文件创建
kubectl apply -f my-pod.yaml
#使用皮遏制文件删除
kubectl delete -f my-pod.yaml
```
标签标签 是附加到对象(比如Pod)上的键值对，用于补充对象的描述信息。
标签使用户能够以松散的方式管理对象映射，而无需客户端存储这些映射。
由于容器有可能广利成千上万个容器，我们可以使用标签高效的进行选择和操作容器集合

- 键值对的格式
   - 前缀(可选)/名称(必须)
- 有效名称和值：
   - 必须为63个字符或更少
   - 如果不为空，必须以字母数字字符([a-z0-9A-Z])开头和结尾
   - 包含破折号-、下滑线_、点. 和字母或数字
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: label-demo
  labels:
    environment: production
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.14.2
    ports:
    - containerPort: 80
```
选择器:::info
标签选择器 可以识别一组对象。标签不支持唯一性
标签选择器最长键的方式Service选择一组Pod作为后端
:::
```shell
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
      # 默认情况下，为了方便起见，`targetPort` 被设置为与 `port` 字段相同的值。
    - port: 80
      targetPort: 80
      # 可选字段
      # 默认情况下，为了方便起见，Kubernetes 控制平面会从某个范围内分配一个端口号（默认：30000-32767）
      nodePort: 30007
```
:::info
目前支持两种标签选择运算：
等值运算
selector:
                 app: nginx
基于集合运算
:::
## 容器与镜像
容器运行时接口kubelet运行在每个节点(Node)上，用于管理和维护Pod和容器的状态。
容器运行时接口(CRI)是kubelet和容器运行时之间通信的主要协议。他将kubelet与容器运行时解耦，理论上实现了CRI接口的容器引擎，都可以作为kubernetes的容器运行时
> Dokcer没有实现(CRI)接口，kubernetes使用dockershim来兼容docker.
> 字v1.24版本起，dockeshim已从kubernetes项目中移除


---

crictl是一个兼容CRi的容器运行时命令，他的用法跟docker名一样，可以用来检查和调试底层容器运行时容器。
```shell
crictl ps
crictl images
```
在一些局域网环境下，我们没法通过互联拉去镜像可以手动导出，导入镜像。
crictl 命令没有导入导出功能
需要使用ctr命令导出导入镜像，他是containerd的命令行接口
```shell
docker save 镜像名称:版本号 >名称-版本.tar
ctr -n k8s.io images import 包  --platform linux/amd64
ctr -n k8s.io images export 全包名  --platform linux/amd64
```
## 金丝雀发布
金丝雀发布金丝雀部署也称灰度发布
你可以在生产环境的基础设施中小范围部署新的代码。一旦应用签署发布，只有少数用户被路由到它，最大限度的降低影响。如果没有番薯错误，则将新版本逐渐推广到整个基础设施
### 部署一个版本
发布v1版本应用，镜像使用nginx:1.22，数量3

- 创建Namespace
   - 创建Namespace配置模板
- 创建Deployment
   - 创建Deployment
- 创建外部访问的Service
   - 创建外部访问Serice
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: dev
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment-v1
  namespace: dev
  labels:
    app: nginx-deployment-v1
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.22
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: canary-demo
  namespace: dev
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
   - port: 80
     targetPort: 80
     nodePort: 30008


```
> **局限性**
> 按照Kubernetes默认支持的这种方式进行金丝雀发布有一定的局限性：
> - 不能根据用户注册时间、地区、等请求中的内容属性进行流量分配
> - 同一个用户如果多次调用该Service、有可能第一次请求到旧版的Pod,第二次请求到新版本的pod
> 
再kubernets中不能解决上述的局限性的原因：kubernetes Service 只在TCP层面解决负载均衡的问题，并不对请求响应的消息做任何解析和识别。如果想要更完善地使用金丝雀发布，可以考虑lstio灰度发布

