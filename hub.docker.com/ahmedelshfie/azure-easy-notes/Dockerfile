# Start with a base image containing Java runtime
FROM openjdk:8-jdk-alpine

# Add Maintainer Info..
MAINTAINER Ahmed Ibrahim Nagi Ali <ahmedelshfie@gmail.com>

# Add a volume pointing to /tmp
VOLUME /tmp

# Make port 8085 available to the world outside this container
EXPOSE 8085

# The application's jar file
ARG JAR_FILE=target/easy-notes-1.0.0.jar

# Add the application's jar to the container
ADD ${JAR_FILE} easy-notes.jar

# Run the jar file 
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/easy-notes.jar"]
