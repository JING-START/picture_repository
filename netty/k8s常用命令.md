[TOC]

###### 1.停止kubelet  ######

systemctl stop kubelet 



###### 2.停止docker 

systemctl stop docker 



###### 3.清空iptables规则 

不是正确方法，生产线上用有风险，测试或虚拟机用没问题 

iptables --flush 
iptables -tnat --flush 



###### 4.启动kubelet 

systemctl start kubelet 

###### 5.启动docker 

systemctl start docker 



###### 6.查看节点信息 

kubectl get nodes 

```
[root@master ~]# kubectl get nodes
NAME     STATUS   ROLES    AGE    VERSION
master   Ready    master   3d1h   v1.19.8
node1    Ready    <none>   2d6h   v1.19.8
```



###### 7.查看所有pod信息 

kubectl get pod --all-namespaces -o wide



###### 8.查看pod日志 

kubectl  -n  <namespace>  logs  <name>

`kubectl -n pie-engine-computing logs computing-messagebus-0` 

kubectl describe  -n <namespaces> pod <name>



###### 9.重启kubelet

systemctl restart kubelet



###### 10.重启docker

systemctl restart docker



###### 11.进入kubelet pod命令

kubectl exec -it  <name> -n <namespaces> /bin/bash 



###### 12.docker删除Exited状态的容器 

docker rm $(docker ps -qf status=exited)



###### 13.docker查看日志

docker logs --tail=1000 <name>



###### 14.查看linux日志

tail -200f /var/log/messages



###### 15.kubectl强制删除pod

kubectl delete pods <pod>  -n <namespace> --grace-period=0 --force



###### 16.kubectl删除job

kubectl delete job <name> -n <namespace>



###### 17查看ClusterIp

kubectl get svc