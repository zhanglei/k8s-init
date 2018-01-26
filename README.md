
# k8s-init

半离线方式部署k8s

解决不能访问  gcr.io ，quay.io ，packages.cloud.google.com 的问题。

淘宝提供k8s部署脚本 k8s-init-v1.9.0.sh，同样 环境下100%部署成功。  

https://item.taobao.com/item.htm?id=561964949540
 

## 部署要求

系统可以访问到 https://files.javablog.net/k8s/ 

目前已测试环境 ubuntu 16.04  ， centos 7.4 , debian 9.3 。master 和 node 机器名不要一样

建议配置至少 2H 2G 20G 纯净系统，连docker都不要装。

## 使用方法 

master上执行 `./k8s-init-v1.9.0.sh master`

拷贝类似如下输出

```
kubeadm join --token c8d946.3ff186c3d9543949 192.168.2.100:6443 --discovery-token-ca-cert-hash sha256:62ac3f587ecaef9b6b924674b9c94e63b75f817c81a6ad500b68b9a4ac7f3b09
```

node上执行 `./k8s-init-v1.9.0.sh node` 

执行完毕后再在node上执行刚拷贝出来的join命令。


### 效果截图

![pod状态](http://wx3.sinaimg.cn/large/006qgpQvly1fmkbcxg1ggj30sb0by0vh.jpg)

![traefik web](http://wx3.sinaimg.cn/large/006qgpQvly1fmkbcxc29aj30u90ndwfz.jpg)

![k8s dashboard](http://wx4.sinaimg.cn/large/006qgpQvly1fmkbcxgxktj31ad0sh41b.jpg)

![部署nginx](https://wx3.sinaimg.cn/mw1024/006qgpQvly1fmkbcxb3sfj30ng0dagm4.jpg)




## 脚本下载地址

https://item.taobao.com/item.htm?id=561964949540


 
 
