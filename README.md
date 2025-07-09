# JIB: Build & Deploy Docker Images with Maven

This project demonstrates how to create a Docker image for a Spring Boot application using the [Jib Maven Plugin](https://github.com/GoogleContainerTools/jib/tree/master/jib-maven-plugin).

Full source code available in the repository: [link](hollow)

## Prerequisites

- Java 17 or later
- Maven 3.x
- Docker installed and running locally
- Docker Hub account with an existing repository (or permission to create one)

## Maven Plugin Configuration

Add the following plugin to the `<plugins>` section of your `pom.xml` file:

```xml
<plugin>
  <groupId>com.google.cloud.tools</groupId>
  <artifactId>jib-maven-plugin</artifactId>
  <version>3.4.3</version>
  <configuration>
    <from>
      <image>openjdk:17-jdk-slim</image>
    </from>
    <to>
      <image>docker.io/your-dockerhub-username/your-repo-name:${project.artifactId}-${project.version}</image>
    </to>
  </configuration>
</plugin>
```

## Authenticate to Docker Hub

Login to Docker Hub from the command line:

```bash
docker login -u your-dockerhub-username
```

You will be prompted to enter your Docker Hub password or access token.

Make sure the Docker repository (e.g., `your-dockerhub-username/your-repo-name`) exists or create it in your Docker Hub account.

## Build and Push the Docker Image

Use the following Maven command to build and push the image directly to Docker Hub:

```bash
mvn clean compile jib:build
```

## Pull and Run the Docker Image (Optional)

To test the image locally, pull it from Docker Hub:

```bash
docker pull your-dockerhub-username/your-repo-name:demo-0.0.1-SNAPSHOT
```

Run the container:

```bash
docker run -p 8080:8080 your-dockerhub-username/your-repo-name:demo-0.0.1-SNAPSHOT
```

Then open a browser and visit:

```
http://localhost:8080/greeting
```

You should see a response from the running Spring Boot application.

## Clean Up Local Docker Resources (Optional)

To remove the container and image from your local system:

```bash
docker ps -a
docker stop <container-id>
docker rm <container-id>
docker images
docker rmi <image-id>
```

Refer to the official Docker CLI documentation or a cheat sheet for more cleanup and management commands.