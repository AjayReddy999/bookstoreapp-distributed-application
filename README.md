# BookStoreApp-Distributed-Application [![HitCount](http://hits.dwyl.io/Ramaseshu0/BookStoreApp-Distributed-Application.svg)](http://hits.dwyl.io/Ramaseshu0/BookStoreApp-Distributed-Application)

---

## About this project
This is an Ecommerce project still "development in progress", where users can add books to the cart and buy those books.

The application is being developed using Java, Spring, and React.

Using Spring Cloud Microservices and Spring Boot Framework extensively to make this application distributed. 

---

## Frontend Checkout Flow
![CheckOutFlow](https://user-images.githubusercontent.com/14878408/103235826-06d5ca00-4969-11eb-87c8-ce618034b4f3.gif)

## Architecture
All the Microservices are developed using Spring Boot. 
These Spring Boot applications will be registered with a Eureka discovery server.

The FrontEnd React App makes requests to an NGINX server which acts as a reverse proxy.
The NGINX server redirects the requests to the Zuul API Gateway. 

Zuul will route the requests to the appropriate microservice based on the URL route. Zuul also registers with Eureka and retrieves the IP/domain from Eureka for the microservice while routing the request. 

---

## Run this project in Local Machine

> Frontend App 

Navigate to the "bookstore-frontend-react-app" folder.
Run the below commands to start the Frontend React Application:

```
yarn install
yarn start
```

> Backend Services

To start Backend Services, follow the steps below using IntelliJ/Eclipse or the Command Line.

Import this project into your IDE and run all Spring Boot projects, or build all the jars by running the "mvn clean install" command in the root parent pom.
All services will be up in the ports mentioned below.

Note: Running the services this way will not provide full monitoring. To see metrics like JVM memory, Tomcat error counts, and other data, use the Docker deployment method.

> Using Docker (Recommended)

1. Start the Docker Engine on your machine.
2. Run "mvn clean install" at the root of the project to build all microservice jars.
3. Run "docker-compose up --build" to start all containers.

Use the "Postman Api collection" in the Postman directory to make requests to various services.

Services will be exposed on these ports:

```
Api Gateway Service       : 8765
Eureka Discovery Service  : 8761
Consul Discovery          : 8500
Account Service           : 4001
Billing Service           : 5001
Catalog Service           : 6001
Order Service             : 7001
Payment Service           : 8001
```

---

### Service Discovery
This project uses Eureka or Consul as the Discovery service.

While running services locally, Eureka is used for service discovery.
While running via Docker, Consul is used for service discovery. 

Consul is utilized in the Docker environment because it offers robust features and support. For local development, Eureka is used to avoid the overhead of managing a local Consul agent.

---

### Troubleshooting

If you encounter any issues while starting up services or if an API fails, it may be due to schema updates. At this stage of development, database migrations are not the primary focus.

If issues persist, try to clear or drop the "bookstore_db". If the problem remains, please raise an issue on GitHub and I will provide assistance.

---

## Deployment (Future Roadmap)
AWS is the intended cloud provider for this project.

The project will be deployed across multiple Regions and Availability Zones. 

The React App, Zuul, and Eureka will be public-facing services located in a public subnet.
All microservices will be containerized and deployed in AWS ECS within a private subnet.

Private subnets will use a NAT Gateway for external internet requests.
A Bastion host can be used to SSH into the private subnet microservices.

Below is the AWS Architecture diagram for reference:

![Bookstore Final](https://user-images.githubusercontent.com/14878408/65784998-000e4500-e171-11e9-96d7-b7c199e74c4c.jpg)

---

## Monitoring
There are two setups available for monitoring:

1. Prometheus and Grafana.
2. TICK stack monitoring.

Both setups are powerful. Prometheus operates on a pull model, where we use Consul discovery to provide target hosts dynamically. This ensures that when new instances are added, they are automatically tracked.

The TICK (Telegraf, InfluxDB, Chronograf, Kapacitor) stack is also supported. InfluxDB serves as the time-series database where services push metrics. Telegraf can also be configured to pull metrics. Chronograf or Grafana can be used for visualization, while Kapacitor handles alerting rules.

The "docker-compose" configuration will handle bringing up all monitoring containers.

Dashboards are available at the following ports:

```
Grafana    : 3030
Zipkin     : 9411
Prometheus : 9090
Telegraf   : 8125
InfluxDb   : 8086
Chronograf : 8888
Kapacitor  : 9092 
```

```
First time login to Grafana:
Username : admin  
Password : admin
```

---

**Screenshots of Tracing in Zipkin**

<img alt="Zipkin" src="https://user-images.githubusercontent.com/14878408/65939069-6b426a80-e442-11e9-90fd-d54b60786d41.png">
<hr>
<img alt="Zipkin" src="https://user-images.githubusercontent.com/14878408/65939165-bb213180-e442-11e9-9ad7-5cfd4fa121ef.png">

---

**Screenshots of Monitoring in Grafana**

<img width="1680" alt="Screen Shot 1" src="https://user-images.githubusercontent.com/14878408/66936473-65ac6d80-f05b-11e9-9e7d-9652059438cd.png">

<img width="1680" alt="Screen Shot 2" src="https://user-images.githubusercontent.com/14878408/66936524-79f06a80-f05b-11e9-8898-1002813aad8e.png">

---

**Screenshots of Monitoring in Chronograf (TICK)**

![Screen Shot 3](https://user-images.githubusercontent.com/14878408/66934353-f8e3a400-f057-11e9-82ab-eda7a230c09d.png)

![Screen Shot 4](https://user-images.githubusercontent.com/14878408/66934482-2e888d00-f058-11e9-8dea-f1f275765265.png)

---

> Account Service

To get an "access_token" for the user, you need the "clientId" and "clientSecret":

```
clientId : '93ed453e-b7ac-4192-a6d4-c45fae0d99ac'
clientSecret : 'client.devd123'
```

There are two users currently configured in the system: ADMIN and NORMAL USER.

```
Admin 
userName: 'admin.admin'
password: 'admin.devd123'
```

```
Normal User 
userName: 'devd.cores'
password: 'cores.devd123'
```

*To get the accessToken (Admin User):* 

```curl 93ed453e-b7ac-4192-a6d4-c45fae0d99ac:client.devd123@localhost:4001/oauth/token -d grant_type=password -d username=admin.admin -d password=admin.devd123```

---

## Maintainer
This project is maintained by Chinmaya Sri Rama Seshu Pasupuleti. Chinmaya is a Data Engineer with over 4 years of experience in building enterprise data pipelines, cloud-based ETL/ELT workflows, and distributed data platforms. This repository serves as a showcase for distributed application architecture and microservices integration.

* GitHub: https://github.com/Ramaseshu0
* LinkedIn: https://www.linkedin.com/in/rama-seshu/
* Email: pramaseshu@outlook.com