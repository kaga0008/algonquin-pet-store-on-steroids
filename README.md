# CST8915 Final project: Best Buy App
## Elizabeth Kaganovsky (040956095)

### Youtube Demo

### Architecture Diagram
![](/CST8915_Final_Architecture.drawio-2.png)

### Brief Architecture Overview
| **Service**      | **Description**                                                                                 | **Language/framework** | **Repo** | **Docker Image** |
|------------------|-------------------------------------------------------------------------------------------------|------------------------|----------|------------------|
| Store-Front      | Front end used by customers to browse products and place orders.                                | Vue.js                 |          |                  |
| Store-Admin      | Front end used by employees to view queued orders from customers and manage available products. | Vue.js                 |          |                  |
| Order-Service    | API for submitting orders from the front end, queues orders in RabbitMQ.                        | Node.js                |          |                  |
| Product-Service  | REST API that performs CRUD operations on products.                                             | Rust                   |          |                  |
| Makeline-Service | REST API for processing orders from the queue and sending them to the database.                 | Go                     |          |                  |
| Database         | MongoDB database that retains order information state fully.                                    | -                      |          |                  |
| Queue            | RabbitMQ message broker that queues orders prior to processing.                                 | -                      |          |                  |
### Deployment instructions

### Links Table