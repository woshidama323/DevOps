# Kubenates 学习
## 常用命令汇总

1. minikube 创建集群


2. kubectl 集群管理工具

```shell
    ## 查看集群中master 和 services的信息
    kubectl cluster-info

    ## 查看kubenate的版本
    kubectl version

    ## 查看集群的配置信息
    kubectl config view

    ## 查看集群可用的api资源
    kubectl api-resources

    ## 查看集群可用的api资源的版本
    kubectl api-versions

    ## 查看集群相关所有信息
    kubectl get all --all-namespaces

    #==  Daemonsets   （干什么用的？）
    ## 查看所有的进程集合
    kubectl get daemonset

    ## 编辑更新一个或多个进程集的定义
    kubectl edit daemonset <daemonset_name>   ## daemonset_name 由上面一个命令获取

    ## 删除daemonset 
    kubectl delete daemonset <daemonset_name>

    ## 创建daemonset
    kubectl create daemonset <daemonset_name>

    ## 管理在线的daemonset
    kubectl rollout daemonset

    ## 通过namespace 查看daemonsets的详细状态
    kubectl describe ds <daemonset_name> -n <namespace_name>
    
    ## == Deployments
    ## 列出一个或者多个deployment
    kubectl get deployment

    ## 列出一个或者多个deployments的详细状态
    kubectl describe deployment <deployment_name>

    ## 编辑更新一个或者多个deployment的定义
    kubectl edit deployment <deployment_name>

    ## 创建一个新的deployment
    kubectl create deployment <deployment_name>

    ## 删除deployment
    kubectl delete deployment <deployment_name>

    ## 查询deployment rollout的状态
    kubectl rollout status deployment <deployment_name>

    ## ==Events
    ## 列出最近当前系统中所有资源的事件
    kubectl get events

    ## 只列出warn级别的事件
    kubectl get events --field-selector type=Warning

    ## 列出出pods之外的所有事件
    kubectl get events --field-selector involvedObject.kind!=Pod

    ## 通过指定名称 列出单个pod的所有事件
    kubectl get events --field-selector involvedObject.kind=Node, involvedObject.name=<node_name>

    ## 从一组事件中过滤出正常的事件
    kubectl get events --field-selector type!=Normal

    ## == logs
    ## 打印一个pod的日志
    kubectl logs <pod_name>

    ## 打印某一个pod最后一小时的日志
    kubectl logs --since=1h <pod_name>

    ## 获取最近20行的log
    kubectl logs --tail=20 <pod_name>

    ## 获取某一个服务的信息，可通过容器过滤
    kubectl logs -f <service_name> [-c <$container>]

    ## tail 最新的pod的日志
    kubectl logs -f <pod_name>

    ## 打印pod中容器的日志
    kubectl logs -c <container_name> <pod_name>

    ## 输出pod的日志到文件中
    kubectl logs <pod_name> pod.log

    ## view logs for a previously failed pod
    kubectl logs --previous <pod_name>

    ## 模糊查询 查找所有的pod_prefix为前缀的日志（https://github.com/johanhaleby/kubetail）
    kubetail <pod_prefix>

    ## 上面最新5分钟的日志
    kubetail <pod_prefix> -s 5m

    ## manifest 文件
    ## 另外可以通过修改mainfest文件来修改对象  强烈推荐 可跟踪修改过程
    kubectl apply -f mainfest_file.yaml

    ## 创建对象
    kubectl create -f mainfest_file.yaml

    ## 通过yaml文件 批量创建对象     dir中存储这yaml文件
    kubectl create -f ./dir

    ## 从url 中获取yaml文件创建对象
    kubectl  create -f url

    ## 删除一个对象
    kubectl delete -f manifest_file.yaml

    ## == Namespaces
    ## 缩写 ns
    ## 创建一个namespace 
    kubectl create namespace <namespace_name>

    ## list一个或者多个namespace
    kubectl get namespace <namespace_name>

    ## 显示一个或者多个namespace详细状态
    kubectl describe namespace <namespace_name>

    ## 删除一个namespace
    kubectl delete namespace <namespace_name>

    ## 编辑一个namespace 
    kubectl edit namespace <namespace_name>

    ## 显示针对一个namespace 的资源使用(CPU/Memory/Storage)
    kubectl top namespace <namespace_name>

    ## == Nodes
    ## 缩写 no
    ## 更新损坏的node ？ 不太对
    kubectl taint node <node_name>

    ## list 一个或者多个nodes
    kubectl get node

    ## 删除一个或者多个node
    kubectl delete node <node_name>

    ## 显示node的资源（cpu/memory/storage）
    kubectl top node

    ## 每一个node的资源分配
    kubectl describe nodes|grep Allocated -A 5

    ## 显示一个node中pods的信息
    kubectl get pods -o wide |grep <node_name>

    ## 为一个node编号
    kubectl annotate node <node_name>

    ## 将一个node标记为不可调度
    kubectl cordon node <node_name>

    ## 标记一个node为可调度
    kubectl uncordon node <node_name>

    ## 排空一个node （向水管一样）准备维护
    kubectl drain node <node_name>

    ## 增加或者更新一个或者多个节点的标签
    kubectl label node

    ## Pods
    ## 缩写 po
    ## list 一个或者多个pod
    kubectl get pod

    ## 删除一个pod 
    kubectl delete pod <pod_name>

    ## 显示pod的当前详细状态
    kubectl describe pod <pod_name>

    ## 创建一个pod
    kubectl create pod <pod_name>

    ## 在指定pod中 某一个容器 执行命令
    kubectl exec <pod_name> -c <container_name> <command>

    ## 进入交互式shell 到指定的单个容器 pod
    kubectl exec -it <pod_name> /bin/bash

    ## 显示资源使用率 针对所有pods
    kubectl top pod

    ## 增加或者更新一个pod的编号
    kubectl annotate pod <pod_name> <annotation>

    ## 增加或者更新一个pod的标签
    kubectl label pod <pod_name>

    ## replication controllers
    ##缩写 rc
    ## list 所有的replication controllers
    kubectl get rc

    ## 通过namespace list replication controllers
    kubectl get rc --namesapce="<namespace_name>"

    ## replicaSets
    ## 缩写 rs
    ## list 所有replicasets
    kubectl get replicasets

    ## 显示一个或者多个replicasets的详细状态
    kubectl describe replicasets <replicaset_name>

    ## 扩展一个replicaset
    kubectl scale --replicas=[x]

    ## secrets
    ## 创建一个secrete
    kubectl create secret

    ## list secrets
    kubectl get secrets

    ## list所有secrets详细信息
    kubectl describe secrets

    ## 删除一个secret
    kubectl delete secret <secret_name>

##  services
    ## 简称 svc
    ## list所有的services
    kubectl get services

    ## 显示一个service的状态
    kubectl describe services

    ## 将一个replication controller service deployment 或者一个pod 作为一个新的kubernates service
    kubectl expose deployment [deployment_name]

    ## 编辑和更新一个或者多个服务的定义
    kubectl edit services

## service accounts
    ## 缩写 sa
    ## list所有的service 账户
    kubectl get serviceaccounts

    ## 显示一个或者多个servcie的账户详细信息
    kubectl describe serviceaccounts

    ## 替换一个service账户
    kubectl replace serviceaccount

    ## 删除一个服务的账户
    kubectl delete serviceaccount <sercie_account_name>

##  statefulset
    ##缩写 sts
    ## list 所有状态集
    kubectl get statefulset

    ## 删除状态集 （不删pods）
    kubectl delete statefulset/[stateful_set_name] --cascade=false

## common options
    ## -o 输出格式 常用的是wide
    kubectl get pods -o wide 
    ## -n 是--namespace的格式
    kubectl get pods --namespace=[namespace_name]
    kubectl get pods -n=[namespace_name]
    ## -f 指定一个文件创建pod
    kubectl create -f ./newpod.json
    ## 


    

```