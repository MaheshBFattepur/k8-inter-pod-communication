# k8-inter-pod-communication
2 Spring boot applications communicate with DNS service discovery from different PODS

# Steps for execution
```
kubectl create -f manifest/deployment.yaml
```
```
kubectl create -f manifests/service.yaml
```

# Verify 
1. kubectl get pods -o wide
```

NAME                                     READY   STATUS    RESTARTS   AGE     IP            NODE        NOMINATED NODE   READINESS GATES
k8-start-deployment-6c9985cd6c-xkplz     1/1     Running   0          4m22s   10.244.3.10   node1.com   <none>           <none>
k8-end-deployment-848fbf696c-mkc87       1/1     Running   0          4s      10.244.3.11   node2.com   <none>           <none>
```
2. kubectl get svc
```

NAME               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
k8-end-service     NodePort    10.104.65.160    <none>        9090:30040/TCP   4m48s
k8-start-service   NodePort    10.106.222.161   <none>        8080:30030/TCP   4m48s
kubernetes         ClusterIP   10.96.0.1        <none>        443/TCP          6d20h
```
3. Open browser and execute http://MASTER-IP:30030/sserver/sayhello
```
O/P: 
Connection established -> [Server: Start, Node: node1.com] Server says hello!!! -> [Server: End, Node: node2.com] Server acknowledge to hello!!! -> Connection closed
```
