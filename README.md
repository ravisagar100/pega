# pega
external kafka testing
### Stream (externalized Kafka service) example with bitnami kafka

For testing purpose you can isntall bitnami kafka using below commands and then bootstrap the URL in the values.yaml file used for Pega Deployment for Stream service

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-release bitnami/kafka
```
Populate the external kafka bootstrapServer URL in the below example
In the below example "mypega" is the namespace where the kafka is deployed, replace with the correct namespace as per your kafka deployment in kubernetes namespace

```
bootstrapServer: "kafka.mypega.svc.cluster.local:9092"
