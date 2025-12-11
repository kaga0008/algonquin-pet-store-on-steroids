# CST8915 Final project: Best Buy App
## Elizabeth Kaganovsky (040956095)

### Youtube Demo

### Architecture Diagram
![](/assets/CST8915_Final_Architectur.png)

### Brief Architecture Overview and Links Table
| **Service**      | **Description**                                                                                 | **Language/framework** | **Repo** | **Docker Image** |
|------------------|-------------------------------------------------------------------------------------------------|------------------------|----------|------------------| 
| Store-Front      | Front end used by customers to browse products and place orders.                                | Vue.js                 | [store-front repo](https://github.com/kaga0008/product-service-L8)         | [store-front image](https://hub.docker.com/repository/docker/kaga0008/store-front-bb/general)                 |
| Store-Admin      | Front end used by employees to view queued orders from customers and manage available products. | Vue.js                 | [store-admin repo](https://github.com/kaga0008/store-admin-L8)        | [store-admin image](https://hub.docker.com/repository/docker/kaga0008/store-admin-bb/general)                 |
| Order-Service    | API for submitting orders from the front end, queues orders in RabbitMQ.                        | Node.js                | [order-service repo](https://github.com/kaga0008/order-service-L8)         | [order-service image](https://hub.docker.com/repository/docker/kaga0008/order-service-bb/general)                 |
| Product-Service  | REST API that performs CRUD operations on products.                                             | Rust                   | [product-service repo](https://github.com/kaga0008/product-service-L8)         | [product-service image](https://hub.docker.com/repository/docker/kaga0008/product-service-bb/general)                 |
| Makeline-Service | REST API for processing orders from the queue and sending them to the database.                 | Go                     | [makeline-service repo](https://github.com/ramymohamed10/makeline-service-L8)        | [makeline-service image](https://hub.docker.com/repository/docker/kaga0008/makeline-service-bb/general)                 |
| Database         | MongoDB database that retains order information state fully.                                    | -                      |          |                  |
| Queue            | RabbitMQ message broker that queues orders prior to processing.                                 | -                      |          |                  |
### Deployment instructions
#### 1. AKS cluster
##### 1.1. Create an AKS cluster with the same configurations as that used in Lab6.
##### 1.2. Connect to the AKS cluster using Azure CLI. As in Lab6, set the cluster subscription and get credentials.
##### 1.3. Confirm cluster connectivity: `kubectl get nodes`

#### 2. Deploy the ConfigMaps
##### 2.1. Apply the ConfigMap for RabbitMQ: `kubectl apply -f config-maps.yaml`
##### 2.2. Verify the ConfigMap deployment: `kubectl get configmaps`

#### 3. Deploy the application
##### 3.1. Deploy the application: `kubectl apply -f best-buy-deploy.yaml`
##### 3.2. Verify the application deployment: `kubectl get pods` and `kubectl get services`

#### 4. Access the application
##### 4.1. Get the external IPs for store-front and store-admin with `kubectl get services`
##### 4.2. Access the store front page at `https://<STORE-FRONT-IP>`
##### 4.3. Access the store admin page at `https://<STORE-ADMIN-IP>`
