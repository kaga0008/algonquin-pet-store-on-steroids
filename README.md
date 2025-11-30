# CST8915 Lab 8
## Elizabeth Kaganovsky (040956095)

### Task 1. Demo Video

### Task 2. 
Repo link: https://github.com/kaga0008/algonquin-pet-store-on-steroids 
#### 2.1. MongoDB Changes
Modifying MongoDB to have three replicas rather than one simply involves updating the number of replicas in the .yaml:
```
replicas: 3
```

For persistent storage, the following it added to the StatefulSet template for MongoDB.
```
volumeClaimTemplates:
    - metadata:                         
        name: mongodb-data              # Template name
    spec:
        accessModes: ["ReadWriteOnce"]  # Multiple pods on the same nodes can access the volume
        resources:
            requests:
                storage: 1Gi            # No idea what a reasonable number here is so 1 GiB it is!
```

And to make the service headless, the following is added to the spec of the service that exposes MongoDB:
```
clusterIP: None
```

#### 2.2. RabbitMQ Changes
In the volumeMounts section of RabbitMQ's StatefulSet, 
```
volumeMounts: # Mount configuration for RabbitMQ plugins
  - name: rabbitmq-enabled-plugins
        mountPath: /etc/rabbitmq/enabled_plugins
        subPath: enabled_plugins
    - name: rabbitmq-data               # <-- Added line 
        mountPath: /var/lib/rabbitmq    # <-- Added line
```

Similar volumeClaimTemplate as that for MongoDB.
```
volumeClaimTemplates:
    - metadata:
        name: rabbitmq-data
    - spec:
        accessModes: ["ReadWriteOnce"]
        resources:
        requests:
            storage: 1Gi
```

#### 2.3. Azure Replacements
**RabbitMQ** - Azure Service Bus makes for a good replacement, as it provides managed message brokering with unmatched scaling (up to millions of requests per second). It also uses the Azure Service Bus Geo-Disaster Recovery to allow processing to continue at another data centre if another becomes unavailable.

**MongoDB** - A ftting replacement would be Azure Cosmos DB for MongoDB, a fully-managed alternative that provides automatic scaling and georeplication while also requiring minimum code changes since it is designed specifically to function like MongoDB.