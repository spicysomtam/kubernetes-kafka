# Introduction

Deploys a kafka stack in kubernetes. Kafka requires zookeeper, so that is included. I include a Yahoo [kafka manager](https://github.com/yahoo/kafka-manager) deployment as well, which allows you to manage kafka.

3 zookeeper instances are deployed and 4 kafka instances. You might want to trim down the kafka replicas if using minikube.

# Deploy zookeeper

```
kubectl create -f zookeeper.yaml
```

# Deploy kafka

Wait for the 3 instances of zookeeper to finish deploying. Then:
```
kubectl create -f kafka.yaml
```

# Deploy kafka-manager

Wait for the  instances of kafka to finish deploying. Then:
```
kubectl create -f kafka-manager.yaml
```

# Accessing kafka-manager

If you are using `minikube`, you might want to change the `kafka-manager` type from `ClusterIP` to `NodePort`. You can edit the running config and change it on the fly (or update `kafka-manager.yaml` and redeploy).

Editing the running config:
```
kubectl edit service/kafka-manager
```

Then you can find the url for the service as follows:
```
minikube service kafka-manager --url
http://192.168.99.100:31957
```
