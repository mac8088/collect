# Develop and Deploy Microservices With JHipster

## Install JHipster 

- Install Java 8 from Oracle:
- Install **Git** from https://git-scm.com:
- Install **Node.js** from http://nodejs.org
- Install **Yarn** using the Yarn installation instructions:
- Run the following command to install Yeoman:
- Run the following command to install JHipster

execute script:

	yarn global add yo
	yarn global add generator-jhipster

## Microservices With JHipster

- Generate a gateway
- Generate a microservice
- Clone the JHipster Registry


We can use the JHipster Console, a monitoring tool based on the ELK Stack. 

## Create an API Gateway

create a blog directory for the gateway application.

	mkdir -p jhipster-microservices-example/blog
	cd jhipster-microservices-example/blog
	jhipster

JHipster prompts you with many questions about the type of application you want to generate and what features you’d like to include. 

Create the blog application with the following settings:

- Application type: Microservice **gateway**
- Base name of the application: blog
- Port: **8080**
- Default package name: org.jhipster.blog
- JHipster Registry: Yes
- Type of authentication: JWT
- Type of database: SQL
- Production database: PostgreSQL
- Development database: H2 with disk-based persistence
- Maven or Gradle: Maven
- Other technologies: **Elasticsearch**
- Client framework: Angular
- Sass for CSS: Yes
- Internationalization support: Yes
- Native language: English
- Additional languages: Spanish
- Testing frameworks: **Gatling, Protractor**
- Install other generators from the JHipster Marketplace: No

Before you can run this project, you’ll need to download and start an instance of the **JHipster Registry**. 

Run the following commands in the jhipster-microservices-example directory.

	git clone git@github.com:jhipster/jhipster-registry.git registry
	cd registry && yarn && ./mvnw


The JHipster Registry is built on Spring Cloud Netflix and Spring Cloud Config. Patterns provided by Spring Cloud Netflix includes:

- Service Discovery (Eureka)
- Circuit Breaker (Hystrix)
- Intelligent Routing (Zuul)
- and Client Side Load Balancing (Ribbon)

JHipster Registry starts on port 8761 by default.


In a new terminal window, navigate to jhipster-microservices-example/blog and run ./mvnw to start the blog application and open http://localhost:8080 in your favorite browser.

- allows you to administer users
- insights into Application and JVM metrics
- allows you to see the Swagger docs associated with its API.

We can run the following command (in a separate terminal window) to start the Protractor tests and confirm everything is working properly.

	yarn e2e

At this point, it’s a good idea to check your project into Git so you can easily see what changes are made going forward.


	git init
	git add .
	git commit -m "Gateway created"


###  Generate Entities


###  Add Business Logic


###  Make UI Enhancements


## Create a Microservice

Create a store directory and run jhipster in it.

	cd ~/jhipster-microservices-example
	mkdir store
	cd store
	jhipster

Use the following settings to generate a microservice that uses MongoDB for its database.

- Application type: **Microservice application**
- Base name of the application: store
- Port: 8081
- Default package name: org.jhipster.store
- Type of authentication: JWT
- Use JHipster Registry: Yes
- Type of database: **MongoDB**
- Maven or Gradle: Maven
- Other technologies: None
- Internationalization support: Yes
- Native language: English
- Additional languages: Spanish
- Testing frameworks: Gatling
- Install other generators from the JHipster Marketplace: No

Commit your changes to Git. It’s always a good idea to do this before generating entities.

	cd ~/jhipster-microservices-example/
	git add store
	git commit -m "Generate store application"

### Generate Product Entity

Create a product entity by running the following command in the store directory.

	jhipster entity product

Use the following answers for the questions asked:

- Do you want to add a field to your entity? Yes
- What is the name of your field? name
- What is the type of your field? **String**
- Do you want to add validation rules to your field? Yes
- Which validation rules do you want to add? **Required**
- Do you want to add a field to your entity? Yes
- What is the name of your field? price
- What is the type of your field? **BigDecimal**
- Do you want to add validation rules to your field? Yes
- Which validation rules do you want to add? **Required**
- Do you want to add a field to your entity? No
- Do you want to use a Data Transfer Object (DTO)? No
- Do you want to use separate service class for your business logic? No
- Do you want pagination on your entity? Yes, with pagination links


### Generate UI for Product Entity

A microservice **only contains the server-side code** for the entities it contains. To generate an Angular UI for the product, navigate to the blog directory and **run the same command**.

	jhipster entity product

Use the following answers to the questions asked:

- Do you want to generate this entity from an existing microservice? Yes
- Enter the path to the microservice root directory: **../store**
- Do you want to update the entity? Yes

Commit your changes to Git.

	cd ~/jhipster-microservices-example
	git add .
	git commit -m "Add product entity"

At this point, you should be able to verify everything works by starting the **registry**, **blog**, **store**, and **MongoDB**.

You can run MongoDB using Docker Compose with the following command in the **store** directory.

	docker-compose -f src/main/docker/mongodb.yml up

### Test

Navigate to http://localhost:8080, log in with **admin/admin**, and go to **Entities > Product**. You should be able to add a product and see that it has a MongoDB identifier.

## Build for Production

A JHipster application can be deployed anywhere a Spring Boot application can be deployed. 

Its Angular client is bundled inside its JAR files.

JHipster ships with support for deploying to Cloud Foundry, Heroku, Kubernetes, AWS, and AWS with Boxfuse.


### prepare a JHipster application for production

When you prepare a JHipster application for production, it’s recommended to use the pre-configured “production” profile. 

With Maven, you can package your application by specifying the prod profile when building.

	./mvnw -Pprod package

The production profile is used to **build an optimized JavaScript client**.


## Deploy to the Cloud

What good is a microservices architecture if it’s not deployed to a PaaS (Platform as a Service)?! 


### Run With Docker Compose

Docker Compose is a tool for defining and running multi-container Docker applications.


1. Make sure Docker is running
2. Build Docker images for the **blog** and **store** applications by running the following command in both directories

the script as bellows:

	./mvnw package -Pprod docker:build

Using your terminal, navigate to the root directory of your project, and create a docker directory. Then run the JHipster Docker Compose sub-generator in it.

	jhipster docker-compose

Here list the questions:

- Application type: Microservice application
- Root directory of your microservices: ../
- Applications to include: blog and store
- Applications with clustered databases: None
- Set up monitoring: JHipster Console with ELK/Zipkin
- The admin password for the JHipster Registry: admin


### Run with Kubernetes and Minikube

To deploy Docker containers with Kubernetes, you set up a cluster, then deploy to it. 

The context can be local (with **Minikube**), or remote (e.g. a Raspberry Pi cluster, Google Cloud, AWS, OpenShift, etc.).

1. Install kubectl, VirtualBox, and Minikube
2. Start Minikube using minikube start
3. To be able to work with the docker daemon, run the following command in your terminal.
4. Create Docker images of the blog and store applications.
5. Using your terminal, navigate to the root directory of your project, and create a kubernetes directory. Then run the 
**JHipster Kubernetes sub-generator** in it.
6. Run the following commands to tag your Docker images. 
7. Run the following commands in the kubernetes directory to deploy to Minikube

script of step3:

	eval $(minikube docker-env)

script of step4:
	
	./mvnw package -Pprod docker:build


script of step5:
	
	jhipster kubernetes

Here list all of questions of step 5:

	Application type: Microservice application
	Root directory of your microservices: ../
	Applications to include: blog and store
	The admin password for the JHipster Registry: admin
	Kubernetes namespace: default
	Base Docker repository name (e.g. mraible): <your-docker-hub-username>
	Command to push Docker image to repository: docker push

script of step6: 

The Kubernetes sub-generator says to run docker push as well, but you don’t need that for a Minikube deployment.

	docker image tag blog mraible/blog
	docker image tag store mraible/store

script of step7:

	kubectl apply -f registry
	kubectl apply -f blog
	kubectl apply -f store

The deployment process can take several minutes to complete. Run minikube dashboard to see the deployed containers.

https://www.jhipster.tech/kubernetes/

You can also run kubectl get po -o wide --watch to see the status of each pod.

To remove all deployed containers, run the following command:

	kubectl delete deployment --all

To stop Minikube, run:
	minikube stop.

To save your changes for Kubernetes, commit your changes to Git from the top-level directory.

	git add .
	git commit -m "Kubernetes"


### Deploy to Google Cloud

