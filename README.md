# **Persona-crud**

**Demo CRUD Microservice - Java 21 + Spring Boot (felcas)**

This project is a sample CRUD microservice developed with Java 21 and Spring Boot 3.x.
Its purpose is to demonstrate a basic microservice architecture with:

**RESTful Endpoints**

Persistence with Spring Data JPA and H2 (in-memory)

Unit tests (JUnit 5 + Mockito + MockMvc)

Coverage report with JaCoCo

CI/CD with Jenkins, SonarQube, and Docker Hub

**Project details**

ArtifactId (pom.xml): persona-crud

Final packaged jar: persona-crud.jar

Docker image (namespace): fmcastre/persona-crud

**Local execution**

Clone the project and build it:

mvn clean package

**Run the tests:**

mvn test

**Start the service:**

mvn spring-boot:run

By default, the service will be available at:
http://localhost:8080/api/persons

**Docker**

Build the image (using the final JAR persona-crud.jar):

mvn clean package
docker build -t fmcastre/persona-crud:latest .

**Run the container:**

docker run -p 8080:8080 fmcastre/persona-crud:latest

# **Technologies and Tools**

Java + Spring Boot: REST backend for CRUD operations

Docker: Containerization of the microservice

Jenkins: CI/CD pipeline automation

SonarQube: Static code quality analysis

Docker Hub: Docker image registry

GitHub: Source code repository

**Key Files**

Dockerfile: Defines how to build the Docker image of the microservice

Jenkinsfile: Contains the declarative pipeline for Jenkins (build, test, analysis, deployment)

sonar-project.properties: Configuration for code analysis in SonarQube

**Automated CI/CD Flow**

The project follows a fully automated CI/CD flow using Jenkins:

Checkout of the code from GitHub:
https://github.com/castrejonfelipe/persona-crud.git

**Build the project using Maven**

Execution of unit tests to ensure basic functionality

Code analysis with SonarQube via the sonar-project.properties file

Building the Docker image with the Dockerfile

Automatic publication to Docker Hub, including tagging with the version or commit hash

**Deployment with Docker**

Once the image is published, you can run the container locally with:

docker pull <your_dockerhub_user>/persona-crud:latest
docker run -p 8080:8080 <your_dockerhub_user>/persona-crud:latest

**Project structure**

<img width="320" height="223" alt="image" src="https://github.com/user-attachments/assets/615c3b45-8e30-42b8-9ea0-733545c3ed9e" />


## **Jenkins Evidence**

This project has continuous integration and automated quality control to ensure the stability and quality of the code.

**Jenkins**
Jenkins is used for the automatic build and testing of the project.
The current build status is shown below.

<img width="1309" height="636" alt="image" src="https://github.com/user-attachments/assets/5a9b3875-6a9c-4645-bcda-47169aaf2252" />


**SonarQube**
Code quality is analyzed with SonarQube, which checks for vulnerabilities, bugs, and test coverage.

  <img width="1135" height="440" alt="image" src="https://github.com/user-attachments/assets/1bcfd885-0f53-4830-874a-676b795e4e54" />


**Docker Hub**
The project's Docker image is published on Docker Hub, making it easy to deploy and distribute.

 <img width="1150" height="605" alt="image" src="https://github.com/user-attachments/assets/3e6d8be0-04e6-465c-865d-997085a04e59" />

**Project**  persona-crud

 <img width="645" height="507" alt="image" src="https://github.com/user-attachments/assets/02a4d9b8-3bd9-47c1-93f9-48e35a9a335a" />

 <img width="644" height="506" alt="image" src="https://github.com/user-attachments/assets/3e333507-7963-4835-96d2-9625d792994e" />

