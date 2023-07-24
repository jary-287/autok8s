# autok8s 
## ansible自动部署kubenetes 集群v1.21.11

## 软件列表
- kubernetes 1.21.11
- nginx v1.20.1
- keepalived v1.3.5
- coredns v1.8
- calico v3.23.5
- containerd v1.6.13
- etcd 3.5

## 部署方式
```shell
git clone git@github.com:jary-287/autok8s.git
cd autok8s
# 修改config.yml
cd playbooks
wget https://dl.k8s.io/v1.21.11/kubernetes-server-linux-amd64.tar.gz -O roles/init_kubernetes/files/kubernetes-server-linux-amd64.tar.gz

wget https://github.com/containerd/containerd/releases/download/v1.6.13/cri-containerd-cni-1.6.13-linux-amd64.tar.gz -O roles/init_kubernetes/files/cri-containerd-cni-1.6.13-linux-amd64.tar.gz

wget https://dl.k8s.io/v1.21.14/kubernetes-node-linux-amd64.tar.gz -O roles/init_kubernetes/files/kubernetes-node-linux-amd64.tar.gz

ansible-playbook deploy.yml   -e "@../config.yml"   -vv
```


## 已知问题
重复部署后需要手动删除网络插件，重新apply。登陆master1节点进行以下操作
```shell
cd /opt/autok8s/ 
kubectl delete -f calico.yml
kubectl apply -f calico.yml
```
