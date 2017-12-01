
# k8s-init

半离线方式部署k8s

解决不能访问  gcr.io ，quay.io ，packages.cloud.google.com 的问题。

## 环境版本

k8s 镜像版本如下  

```
root@k8s-master:~# docker images
REPOSITORY                                               TAG                 IMAGE ID            CREATED             SIZE
gcr.io/google_containers/kube-apiserver-amd64            v1.8.4              10a052dccbc5        6 days ago          194 MB
gcr.io/google_containers/kube-controller-manager-amd64   v1.8.4              7058ac4d4af5        6 days ago          129 MB
gcr.io/google_containers/kube-proxy-amd64                v1.8.4              65a61c14e8c2        6 days ago          93.2 MB
gcr.io/google_containers/kube-scheduler-amd64            v1.8.4              0d985fed7f95        6 days ago          55 MB
quay.io/coreos/flannel                                   v0.9.1-amd64        2b736d06ca4c        9 days ago          51.3 MB
gcr.io/google_containers/kubernetes-dashboard-amd64      v1.7.1              294879c6444e        7 weeks ago         128 MB
gcr.io/google_containers/k8s-dns-sidecar-amd64           1.14.5              fed89e8b4248        2 months ago        41.8 MB
gcr.io/google_containers/k8s-dns-kube-dns-amd64          1.14.5              512cd7425a73        2 months ago        49.4 MB
gcr.io/google_containers/k8s-dns-dnsmasq-nanny-amd64     1.14.5              459944ce8cc4        2 months ago        41.4 MB
gcr.io/google_containers/etcd-amd64                      3.0.17              243830dae7dd        9 months ago        169 MB
gcr.io/google_containers/pause-amd64                     3.0                 99e59f495ffa        19 months ago       747 kB

```
 

部署要求

系统可以访问到 https://files.javablog.net/k8s/ 

目前只支持  ubuntu 16.04 x64 

建议 2H 4G 20G 纯净系统

## 使用方法 

### master节点  

测试环境   192.168.2.100

`./k8s-init.sh master`

拷贝类似如下输出

```
kubeadm join --token c8d946.3ff186c3d9543949 192.168.2.100:6443 --discovery-token-ca-cert-hash sha256:62ac3f587ecaef9b6b924674b9c94e63b75f817c81a6ad500b68b9a4ac7f3b09
```

检查pod状态,务必等待全都是Running的状态再去初始化node节点。


```
root@k8s-master:~# kubectl get pod --all-namespaces

NAMESPACE     NAME                                 READY     STATUS    RESTARTS   AGE
kube-system   etcd-k8s-master                      1/1       Running   0          3m
kube-system   kube-apiserver-k8s-master            1/1       Running   0          3m
kube-system   kube-controller-manager-k8s-master   1/1       Running   0          3m
kube-system   kube-dns-545bc4bfd4-4dw5z            3/3       Running   0          4m
kube-system   kube-flannel-ds-zh99l                1/1       Running   1          4m
kube-system   kube-proxy-ssb4f                     1/1       Running   0          4m
kube-system   kube-scheduler-k8s-master            1/1       Running   0          3m
```


### node节点   

测试环境 192.168.2.101

`./k8s-init.sh node`

初始化脚本执行完毕之后master节点输出的join命令，再回到master检查node状态。

`root@k8s-master:~# kubectl get node --all-namespaces`

此时应该能看到两个Ready

```
root@k8s-master:~# kubectl get node
NAME         STATUS    ROLES     AGE       VERSION
k8s-master   Ready     master    7m        v1.8.4
k8s-node     Ready     <none>    37s       v1.8.4

```

pod也能看到多出了proxy和flannel

```
root@k8s-master:~# kubectl get pod --all-namespaces
NAMESPACE     NAME                                 READY     STATUS    RESTARTS   AGE
kube-system   etcd-k8s-master                      1/1       Running   0          8m
kube-system   kube-apiserver-k8s-master            1/1       Running   0          8m
kube-system   kube-controller-manager-k8s-master   1/1       Running   0          8m
kube-system   kube-dns-545bc4bfd4-cp2c6            3/3       Running   0          8m
kube-system   kube-flannel-ds-2shds                1/1       Running   0          1m
kube-system   kube-flannel-ds-584jj                1/1       Running   0          8m
kube-system   kube-proxy-fxdgw                     1/1       Running   0          1m
kube-system   kube-proxy-hcz7n                     1/1       Running   0          8m
kube-system   kube-scheduler-k8s-master            1/1       Running   0          8m

```

后续就可以部署自己的应用了。

## 部署helloworld

```
root@k8s-master:~# kubectl apply -f https://raw.githubusercontent.com/jolestar/kubernetes-complete-course/master/example/helloworld.yaml 
deployment "helloworld" created
service "helloworld" created
root@k8s-master:~# kubectl -n default get svc helloworld 
NAME         TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
helloworld   NodePort   10.102.79.229   <none>        80:30723/TCP   8s
```


![部署效果](https://files.javablog.net/k8s/k8s-helloworld.png)

## 脚本下载地址

https://item.taobao.com/item.htm?id=561964949540


## 脚本使用问题微信联系 


![微信](https://files.javablog.net/k8s/%E5%BE%AE%E4%BF%A1%E8%81%94%E7%B3%BB%E6%88%91.jpg)

from k8s  









