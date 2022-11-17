# pega
### Stream (externalized Kafka service) example with bitnami kafka

For testing purpose you can install bitnami kafka using below commands 

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-kafka bitnami/kafka
```
Once you deploy external kafka you can populate the external kafka bootstrapServer URL and then bootstrap in the values.yaml file used for Pega Deployment for Stream service.
In the below example "my-kafka" is the release name and "mypega" is the namespace where the kafka is deployed, replace with the correct namespace as per your kafka deployment in kubernetes namespace

```
bootstrapServer: "my-kafka.mypega.svc.cluster.local:9092"
