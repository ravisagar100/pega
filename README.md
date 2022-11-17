### Stream (externalized Kafka service) test example with bitnami kafka

For testing purpose you can install bitnami kafka using below commands 

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-kafka bitnami/kafka
```
After you deploy a Kafka service in your organization, you can populate the service's Kafka `bootstrapServer` URL. You configure the bootstrap URL in the Pega `values.yaml` file in the `Stream (externalized Kafka service) settings`
section to establish connectivity between Pega and your Kafka cluster as shown in the following example .
In the example, in the `bootstrapServer` parameter, "my-kafka" is the release name and "mypega" is the namespace of the Pega deployment. For your deployment, replace this general example with the specific release name and namespace. When your deployment starts it connects to your Kafka service.

```
# Stream (externalized Kafka service) settings.
stream:
  # Disabled by default, when enabled, your deployment no longer uses the "Stream" node type.
  enabled: true
  # Provide externalized Kafka service broker urls.
  bootstrapServer: "my-kafka.mypega.svc.cluster.local:9092"
  # Provide Security Protocol used to communicate with kafka brokers. Supported values are: PLAINTEXT, SSL, SASL_PLAINTEXT, SASL_SSL.
  securityProtocol: PLAINTEXT
  # If required, provide trustStore certificate file name
  # When using a trustStore certificate, you must also include a Kubernetes secret name, that contains the trustStore certificate,
  # in the global.certificatesSecrets parameter.
  # Pega deployments only support trustStores using the Java Key Store (.jks) format.
  trustStore: ""
  # If required provide trustStorePassword value in plain text.
  trustStorePassword: ""
  # If required, provide keyStore certificate file name
  # When using a keyStore certificate, you must also include a Kubernetes secret name, that contains the keyStore certificate,
  # in the global.certificatesSecrets parameter.
  # Pega deployments only support keyStores using the Java Key Store (.jks) format.
  keyStore: ""
  # If required, provide keyStore value in plain text.
  keyStorePassword: ""
  # If required, provide jaasConfig value in plain text.
  jaasConfig: ""
  # If required, provide a SASL mechanism**. Supported values are: PLAIN, SCRAM-SHA-256, SCRAM-SHA-512.
  saslMechanism: PLAIN
  # By default, topics originating from Pega Platform have the pega- prefix,
  # so that it is easy to distinguish them from topics created by other applications.
  # Pega supports customizing the name pattern for your Externalized Kafka configuration for each deployment.
  streamNamePattern: "pega-{stream.name}"
  # Your replicationFactor value cannot be more than the number of Kafka brokers and 3.
  replicationFactor: "1"
  # To avoid exposing trustStorePassword, keyStorePassword, and jaasConfig parameters, leave the values empty and
  # configure them using an External Secrets Manager, making sure you configure the keys in the secret in the order:
  # STREAM_TRUSTSTORE_PASSWORD, STREAM_KEYSTORE_PASSWORD and STREAM_JAAS_CONFIG.
  # Enter the external secret name below.
  external_secret_name: ""
