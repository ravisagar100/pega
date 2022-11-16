# pega
### Stream (externalized Kafka service) example with bitnami kafka

For testing purpose you can install bitnami kafka using below commands 

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-release bitnami/kafka
```
Populate the external kafka bootstrapServer URL and then bootstrap in the values.yaml file used for Pega Deployment for Stream service.
In the below example "mypega" is the namespace where the kafka is deployed, replace with the correct namespace as per your kafka deployment in kubernetes namespace

```
bootstrapServer: "kafka.mypega.svc.cluster.local:9092"
