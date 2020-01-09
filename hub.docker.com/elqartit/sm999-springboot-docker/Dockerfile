FROM maven:3.2-jdk-8

VOLUME /tmp

WORKDIR /sm999-springboot-docker

# Prepare by downloading dependencies
ADD pom.xml /sm999-springboot-docker/pom.xml  
#RUN ["mvn", "dependency:resolve"]
#RUN ["mvn", "verify"]

# Adding source, compile and package into a fat jar
ADD src /sm999-springboot-docker/src
RUN ["mvn", "clean", "install"]

RUN ["ls", "/sm999-springboot-docker/target"]
RUN ["pwd"]
RUN ["ls", "-ltrh", "/sm999-springboot-docker/target/sm999-springboot-docker-2.0.0-SNAPSHOT.jar"]

EXPOSE 8082

ENTRYPOINT [ "java", "-jar", "/sm999-springboot-docker/target/sm999-springboot-docker-2.0.0-SNAPSHOT.jar" ]


# Start with a base image containing Java runtime
#FROM openjdk:8-jdk-alpine

# Add Maintainer Info
#LABEL maintainer="elqartit@gmail.com"

# Add a volume pointing to /tmp
#VOLUME /tmp

# Make port 8080 available to the world outside this container
#EXPOSE 8081

# The application's jar file
#ARG JAR_FILE=sm999-springboot-docker-1.0.0-SNAPSHOT.jar

# Add the application's jar to the container
#ADD ${JAR_FILE} sm999-springboot-docker.jar

# Run the jar file 
#ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/sm999-springboot-docker.jar"]