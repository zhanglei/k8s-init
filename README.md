
# k8s-init

半离线方式部署k8s

解决不能访问  gcr.io ，quay.io ，packages.cloud.google.com 的问题。

淘宝提供k8s部署脚本 k8s-init-v1.9.3.sh，同样 环境下100%部署成功。  

https://item.taobao.com/item.htm?id=561964949540
 

## 部署要求

系统可以访问到 https://files.javablog.net/k8s/ 

目前已测试环境 ubuntu 16.04  ， centos 7.4 , debian 9.3 。master 和 node 机器名不要一样

建议配置至少 2H 2G 20G 纯净系统，连docker都不要装。

## 使用方法 

master上执行 `./k8s-init-v1.9.3.sh master`

拷贝类似如下输出

```
kubeadm join --token c8d946.3ff186c3d9543949 192.168.2.100:6443 --discovery-token-ca-cert-hash sha256:62ac3f587ecaef9b6b924674b9c94e63b75f817c81a6ad500b68b9a4ac7f3b09
```

node上执行 `./k8s-init-v1.9.3.sh node` 

执行完毕后再在node上执行刚拷贝出来的join命令。


### 效果截图


![console](https://img.alicdn.com/imgextra/i2/62227140/TB2sqNUXzQnBKNjSZSgXXXHGXXa_!!62227140.png)

![dashboard](https://img.alicdn.com/imgextra/i3/62227140/TB26g0TXtcnBKNjSZR0XXcFqFXa_!!62227140.png)




## 脚本下载地址

https://item.taobao.com/item.htm?id=561964949540


 
 
