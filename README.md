# k8-roboshop
Roboshop application using Kubernetes


## Mongodb

```shell
$ kubectl apply -f manifest.yaml
deployment.apps/mongodb created
service/mongodb created

$ kubectl get deployment -n roboshop
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
mongodb   3/3     3            3           76s

$ kubectl get rs -n roboshop
NAME                 DESIRED   CURRENT   READY   AGE
mongodb-6589f5667b   3         3         3       84s

$ kubectl get pods -n roboshop -o wide
NAME                       READY   STATUS    RESTARTS   AGE    IP               NODE                             NOMINATED NODE   READINESS GATES
mongodb-6589f5667b-bftg4   1/1     Running   0          3m3s   192.168.41.18    ip-192-168-55-228.ec2.internal   <none>           <none>
mongodb-6589f5667b-m4gxg   1/1     Running   0          3m3s   192.168.31.72    ip-192-168-12-35.ec2.internal    <none>           <none>
mongodb-6589f5667b-wsk4r   1/1     Running   0          3m3s   192.168.20.173   ip-192-168-12-35.ec2.internal    <none>           <none>

If we see the IPs of the POD will add as an endpoints to the service

$ kubectl describe svc mongodb -n roboshop
Name:                     mongodb
Namespace:                roboshop
Labels:                   component=mongodb
                          project=rosboshop
                          tier=database
Annotations:              <none>
Selector:                 component=mongodb,project=rosboshop,tier=database
Type:                     ClusterIP
IP:                       10.100.140.73
IPs:                      10.100.140.73
Port:                     <unset>  27017/TCP
TargetPort:               27017/TCP
Endpoints:                192.168.41.18:27017,192.168.20.173:27017,192.168.31.72:27017
Session Affinity:         None
Internal Traffic Policy:  Cluster
Events:                   <none>

```