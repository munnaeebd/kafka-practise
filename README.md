# kafka-practise

https://learnk8s.io/kafka-ha-kubernetes

https://docs.bitnami.com/tutorials/deploy-scalable-kafka-zookeeper-cluster-kubernetes/


*  Here's a YAML manifest, kafka.yaml, defining the resources required to create a simple Kafka cluster, There is a StatefulSet with three ready Kafka broker pods and a service. 3 PV will be required to create manually. 

* Combining a StatefulSet with a Headless Service. A Service with clusterIP: None is usually called a Headless Service. 
So, how do you use it? A headless service is helpful in combination with CoreDNS. When you issue a DNS query to a standard ClusterIP service, you receive a single IP address: However, when you query a Headless service, the DNS replies with all of the individual IP addresses of the Pods (in this case, the service has two pods):

* From inside the cluster and same name space we can use service name (headless service), or include namespace name from different namespace. 
* add a individual label to the individual pod ; kafka-set-component: kafka-1 ; for kafka pod 1 , kafka-set-component: kafka-2 for kafka pod 2....
```
  labels:
    app: kafka-app
    controller-revision-hash: kafka-64d9466dc9
    kafka-set-component: kafka-1
```

* kafka1-svc.yaml it will point to specific pod. set "externalTrafficPolicy: Local" to make sure nodeport will reply/listen only from the specific node the kafka pod is running . 

```
spec:
  clusterIP: 10.103.134.123
  clusterIPs:
  - 10.103.134.123
  externalTrafficPolicy: Local
```
