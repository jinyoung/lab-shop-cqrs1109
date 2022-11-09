# 

## Model
www.msaez.io/#/courses/cna-full/e016ae10-5e2f-11ed-8df5-9bfd9fa68774/dp-graphql-2022

## Before Running Services
### Make sure there is a Infra running (kafka, mysql, cdc)
```
cd infra
docker-compose up
```
- Watch the MySQL messages:
```
docker exec -it infra-mysql-1 /bin/bash

mysql --user=root --password=$MYSQL_ROOT_PASSWORD
use eventuate;
select * from message;
```
- Watch the Kafka messages:
```
docker exec -it infra-kafka-1 /bin/bash
cd /bin

./kafka-console-consumer --bootstrap-server localhost:9092 --topic README.md.domain.{aggregate name}
```
> Aggregate Names:
- Order
- Inventory
- Delivery


## Run the backend micro-services
See the README.md files inside the each microservices directory:

- order
- inventory
- delivery
- customercenter


## Run API Gateway (Spring Gateway)
```
cd gateway
mvn spring-boot:run
```

## Test by API
- order
```
 http :8088/orders id="id" productId="productId" qty="qty" customerId="customerId" amount="amount" status="status" address="address" 
```
- inventory
```
 http :8088/inventories id="id" stock="stock" 
```
- delivery
```
 http :8088/deliveries id="id" address="address" customerId="customerId" quantity="quantity" orderId="orderId" 
```
- customercenter
```
```


## Run the frontend
```
cd frontend
npm i
npm run serve
```

## Test by UI
Open a browser to localhost:8088

## Required Utilities

- httpie (alternative for curl / POSTMAN) and network utils
```
sudo apt-get update
sudo apt-get install net-tools
sudo apt install iputils-ping
pip install httpie
```

- kubernetes utilities (kubectl)
```
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

- aws cli (aws)
```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

- eksctl 
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
```

