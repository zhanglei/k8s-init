
# k8s-init

半离线方式部署k8s

解决不能访问  gcr.io ，quay.io ，packages.cloud.google.com 的问题。

视频教程  链接: https://pan.baidu.com/s/1bo5Vh1t 密码: gs2f



## 部署要求

系统可以访问到 https://files.javablog.net/k8s/ 

目前只支持  ubuntu 16.04 x64  ， master 和 node 机器名不要一样

建议 2H 2G 20G 纯净系统

## 使用方法 

master上执行 `./k8s-init-v1.9.0.sh master`

拷贝类似如下输出

```
kubeadm join --token c8d946.3ff186c3d9543949 192.168.2.100:6443 --discovery-token-ca-cert-hash sha256:62ac3f587ecaef9b6b924674b9c94e63b75f817c81a6ad500b68b9a4ac7f3b09
```

node上执行 `./k8s-init-v1.9.0.sh node` 

执行完毕后再执行 master 上输出的join命令。


### 效果截图

![pod状态](http://wx3.sinaimg.cn/large/006qgpQvly1fmkbcxg1ggj30sb0by0vh.jpg)

![traefik web](http://wx3.sinaimg.cn/large/006qgpQvly1fmkbcxc29aj30u90ndwfz.jpg)

![k8s dashboard](http://wx4.sinaimg.cn/large/006qgpQvly1fmkbcxgxktj31ad0sh41b.jpg)

![部署nginx](https://wx3.sinaimg.cn/mw1024/006qgpQvly1fmkbcxb3sfj30ng0dagm4.jpg)




## 脚本下载地址

https://item.taobao.com/item.htm?id=561964949540


## 脚本使用问题微信联系 


![微信](https://files.javablog.net/k8s/%E5%BE%AE%E4%BF%A1%E8%81%94%E7%B3%BB%E6%88%91.jpg)

from k8s  


