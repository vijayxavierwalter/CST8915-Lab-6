# Kubectl Command Verification Report

## Environment
- **Operating System:** Microsoft Windows 10
- **Cluster Type:** Azure Kubernetes Service (AKS)

## 1. `kubectl cluster-info`

```text
C:\Users\vijay>kubectl cluster-info
Kubernetes control plane is running at https://algonquinpetstorecluster-dns-oipz72ak.hcp.canadacentral.azmk8s.io:443
CoreDNS is running at https://algonquinpetstorecluster-dns-oipz72ak.hcp.canadacentral.azmk8s.io:443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
Metrics-server is running at https://algonquinpetstorecluster-dns-oipz72ak.hcp.canadacentral.azmk8s.io:443/api/v1/namespaces/kube-system/services/https:metrics-server:/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

## 2. `kubectl get nodes`

```text
C:\Users\vijay>kubectl get nodes
NAME                                 STATUS   ROLES    AGE    VERSION
aks-masterpool-19574420-vmss000000   Ready    <none>   115m   v1.33.7
aks-workerspool-19574420-vms1        Ready    <none>   115m   v1.33.7
```

## 3. `kubectl get pods`

```text
C:\Users\vijay>kubectl get pods
NAME                               READY   STATUS    RESTARTS   AGE
order-service-576b69964f-hqc7j     1/1     Running   0          78m
product-service-6d677dbbcb-vmzd5   1/1     Running   0          78m
rabbitmq-76fb68cc9d-hs84d          1/1     Running   0          78m
store-front-86d4bf757c-dxmfs       1/1     Running   0          78m
```

## 4. `kubectl get services`

```text
C:\Users\vijay>kubectl get services
NAME              TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)              AGE
kubernetes        ClusterIP      10.0.0.1       <none>        443/TCP              116m
order-service     ClusterIP      10.0.56.152    <none>        3000/TCP             79m
product-service   ClusterIP      10.0.211.96    <none>        3030/TCP             79m
rabbitmq          ClusterIP      10.0.88.56     <none>        5672/TCP,15672/TCP   79m
store-front       LoadBalancer   10.0.217.124   4.172.1.197   80:31417/TCP         79m
```

## 5. `kubectl describe pod order-service-576b69964f-hqc7j`

```text
C:\Users\vijay>kubectl describe pod order-service-576b69964f-hqc7j
Name:             order-service-576b69964f-hqc7j
Namespace:        default
Priority:         0
Service Account:  default
Node:             aks-masterpool-19574420-vmss000000/10.224.0.4
Start Time:       Wed, 18 Mar 2026 18:10:34 -0400
Labels:           app=order-service
                  pod-template-hash=576b69964f
Annotations:      <none>
Status:           Running
IP:               10.244.0.187
IPs:
  IP:           10.244.0.187
Controlled By:  ReplicaSet/order-service-576b69964f
Containers:
  order-service:
    Container ID:   containerd://d1b15b5739304a538ddc5b1662ac971b3c5cf25d362757a648f38ca00274ba70
    Image:          ramymohamed/order-service:latest
    Image ID:       docker.io/ramymohamed/order-service@sha256:21f43fdbabc2a1a484bcc31467585c4a7020a531bb67d8c8cf7bf7ef90e04140
    Port:           3000/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Wed, 18 Mar 2026 18:10:40 -0400
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:     200m
      memory:  256Mi
    Requests:
      cpu:     100m
      memory:  128Mi
    Environment:
      RABBITMQ_CONNECTION_STRING:  amqp://myuser:mypassword@rabbitmq:5672/
      PORT:                        3000
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-mcbj8 (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-mcbj8:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/memory-pressure:NoSchedule op=Exists
                             node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:                      <none>
```

## 6. `kubectl describe pod product-service-6d677dbbcb-vmzd5`

```text
C:\Users\vijay>kubectl describe pod product-service-6d677dbbcb-vmzd5
Name:             product-service-6d677dbbcb-vmzd5
Namespace:        default
Priority:         0
Service Account:  default
Node:             aks-masterpool-19574420-vmss000000/10.224.0.4
Start Time:       Wed, 18 Mar 2026 18:10:34 -0400
Labels:           app=product-service
                  pod-template-hash=6d677dbbcb
Annotations:      <none>
Status:           Running
IP:               10.244.0.119
IPs:
  IP:           10.244.0.119
Controlled By:  ReplicaSet/product-service-6d677dbbcb
Containers:
  product-service:
    Container ID:   containerd://cc6708fa92cffd17d4c26b7609652093386deebfc81500bca553120a189a41ff
    Image:          ramymohamed/product-service:latest
    Image ID:       docker.io/ramymohamed/product-service@sha256:942983d37f955366f0ef5a141f391a20c689b1c36793b55c073cc064e3e9f906
    Port:           3030/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Wed, 18 Mar 2026 18:10:39 -0400
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:     200m
      memory:  256Mi
    Requests:
      cpu:     100m
      memory:  128Mi
    Environment:
      PORT:  3030
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-gg222 (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-gg222:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/memory-pressure:NoSchedule op=Exists
                             node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:                      <none>
```

## 7. `kubectl describe pod rabbitmq-76fb68cc9d-hs84d`

```text
C:\Users\vijay>kubectl describe pod rabbitmq-76fb68cc9d-hs84d
Name:             rabbitmq-76fb68cc9d-hs84d
Namespace:        default
Priority:         0
Service Account:  default
Node:             aks-workerspool-19574420-vms1/10.224.0.5
Start Time:       Wed, 18 Mar 2026 18:10:34 -0400
Labels:           app=rabbitmq
                  pod-template-hash=76fb68cc9d
Annotations:      <none>
Status:           Running
IP:               10.244.1.217
IPs:
  IP:           10.244.1.217
Controlled By:  ReplicaSet/rabbitmq-76fb68cc9d
Containers:
  rabbitmq:
    Container ID:   containerd://72d936f9f4547700299c9590ed8dd89ebe2c2d0aeb814cb2d00ca876b65c84ef
    Image:          rabbitmq:3-management
    Image ID:       docker.io/library/rabbitmq@sha256:e582c0bc7766f3342496d8485efb5a1df782b5ce3886ad017e2eaae442311f69
    Ports:          5672/TCP, 15672/TCP
    Host Ports:     0/TCP, 0/TCP
    State:          Running
      Started:      Wed, 18 Mar 2026 18:10:39 -0400
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:     500m
      memory:  512Mi
    Requests:
      cpu:     250m
      memory:  256Mi
    Environment:
      RABBITMQ_DEFAULT_USER:                myuser
      RABBITMQ_DEFAULT_PASS:                mypassword
      RABBITMQ_SERVER_ADDITIONAL_ERL_ARGS:  -rabbitmq_management path_prefix "/rabbitmq"
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-xx2gn (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-xx2gn:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/memory-pressure:NoSchedule op=Exists
                             node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:                      <none>
```

## 8. `kubectl describe pod store-front-86d4bf757c-dxmfs`

```text
C:\Users\vijay>kubectl describe pod store-front-86d4bf757c-dxmfs
Name:             store-front-86d4bf757c-dxmfs
Namespace:        default
Priority:         0
Service Account:  default
Node:             aks-masterpool-19574420-vmss000000/10.224.0.4
Start Time:       Wed, 18 Mar 2026 18:10:34 -0400
Labels:           app=store-front
                  pod-template-hash=86d4bf757c
Annotations:      <none>
Status:           Running
IP:               10.244.0.108
IPs:
  IP:           10.244.0.108
Controlled By:  ReplicaSet/store-front-86d4bf757c
Containers:
  store-front:
    Container ID:   containerd://1500a0a9148f64a7d6084255fcb9ff9320bdf85ab22b0488028953f692a00f93
    Image:          ramymohamed/store-front:latest
    Image ID:       docker.io/ramymohamed/store-front@sha256:1bd94304681bc8ee1d0635d657c7dd5ab3ef411ddbf620ccac5cd81345849e4f
    Port:           80/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Wed, 18 Mar 2026 18:10:39 -0400
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:     200m
      memory:  256Mi
    Requests:
      cpu:        100m
      memory:     128Mi
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-ld6zj (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True
  Initialized                 True
  Ready                       True
  ContainersReady             True
  PodScheduled                True
Volumes:
  kube-api-access-ld6zj:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/memory-pressure:NoSchedule op=Exists
                             node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:                      <none>
```

## 9. `kubectl logs store-front-86d4bf757c-dxmfs`

```text
C:\Users\vijay>kubectl logs store-front-86d4bf757c-dxmfs
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: /etc/nginx/conf.d/default.conf differs from the packaged version
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/03/18 22:10:39 [notice] 1#1: using the "epoll" event method
2026/03/18 22:10:39 [notice] 1#1: nginx/1.29.6
2026/03/18 22:10:39 [notice] 1#1: built by gcc 15.2.0 (Alpine 15.2.0)
2026/03/18 22:10:39 [notice] 1#1: OS: Linux 5.15.0-1102-azure
2026/03/18 22:10:39 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2026/03/18 22:10:39 [notice] 1#1: start worker processes
2026/03/18 22:10:39 [notice] 1#1: start worker process 29
2026/03/18 22:10:39 [notice] 1#1: start worker process 30
10.224.0.4 - - [18/Mar/2026:22:17:57 +0000] "GET / HTTP/1.1" 200 648 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36 Edg/146.0.0.0" "-"
10.224.0.4 - - [18/Mar/2026:22:18:06 +0000] "POST /orders HTTP/1.1" 200 14 "http://4.172.1.197/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36 Edg/146.0.0.0" "-"
10.224.0.4 - - [18/Mar/2026:22:19:27 +0000] "GET /rabbitmq/ HTTP/1.1" 200 1634 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36 Edg/146.0.0.0" "-"
10.224.0.5 - myuser [18/Mar/2026:22:19:49 +0000] "GET /rabbitmq/api/whoami HTTP/1.1" 200 66 "http://4.172.1.197/rabbitmq/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36 Edg/146.0.0.0" "-"
10.224.0.5 - myuser [18/Mar/2026:22:20:00 +0000] "POST /rabbitmq/api/queues/%2F/order_queue/get HTTP/1.1" 200 269 "http://4.172.1.197/rabbitmq/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36 Edg/146.0.0.0" "-"
```

## 10. `kubectl get all`

```text
C:\Users\vijay>kubectl get all
NAME                                   READY   STATUS    RESTARTS   AGE
pod/order-service-576b69964f-hqc7j     1/1     Running   0          81m
pod/product-service-6d677dbbcb-vmzd5   1/1     Running   0          81m
pod/rabbitmq-76fb68cc9d-hs84d          1/1     Running   0          81m
pod/store-front-86d4bf757c-dxmfs       1/1     Running   0          81m

NAME                      TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)              AGE
service/kubernetes        ClusterIP      10.0.0.1       <none>        443/TCP              118m
service/order-service     ClusterIP      10.0.56.152    <none>        3000/TCP             81m
service/product-service   ClusterIP      10.0.211.96    <none>        3030/TCP             81m
service/rabbitmq          ClusterIP      10.0.88.56     <none>        5672/TCP,15672/TCP   81m
service/store-front       LoadBalancer   10.0.217.124   4.172.1.197   80:31417/TCP         81m

NAME                              READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/order-service     1/1     1            1           81m
deployment.apps/product-service   1/1     1            1           81m
deployment.apps/rabbitmq          1/1     1            1           81m
deployment.apps/store-front       1/1     1            1           81m

NAME                                         DESIRED   CURRENT   READY   AGE
replicaset.apps/order-service-576b69964f     1         1         1       81m
replicaset.apps/product-service-6d677dbbcb   1         1         1       81m
replicaset.apps/rabbitmq-76fb68cc9d          1         1         1       81m
replicaset.apps/store-front-86d4bf757c       1         1         1       81m
```

## 11. `kubectl get deployments`

```text
C:\Users\vijay>kubectl get deployments
NAME              READY   UP-TO-DATE   AVAILABLE   AGE
order-service     1/1     1            1           81m
product-service   1/1     1            1           81m
rabbitmq          1/1     1            1           81m
store-front       1/1     1            1           81m
```
## How this setup is possible  
The updated store-front application uses Nginx as a reverse proxy. The Dockerfile builds the Vue frontend and packages it into an Nginx image with a custom nginx.conf. In that configuration, the root path / serves the frontend files, while /products, /orders, and /rabbitmq/ are proxied to the internal Kubernetes services product-service:3030, order-service:3000, and rabbitmq:15672. This allows multiple application components to be accessed through the same external IP address (`4.172.1.197`), with Nginx routing traffic by URL path 

## Summary
The essential `kubectl` commands were tested successfully on the AKS cluster. All application pods are in the **Running** state, all deployments are **Available**, and the **store-front** service has a public **LoadBalancer** IP address (`4.172.1.197`), confirming that the Algonquin Pet Store application was deployed successfully.
