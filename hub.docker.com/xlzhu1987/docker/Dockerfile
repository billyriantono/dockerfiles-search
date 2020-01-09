# Use Java as base image
FROM openjdk:8-alpine

# Add Jar package into container and rename
ADD src/main/resources/application.yml application.yml
ADD target/SpringBootApp-0.0.1-SNAPSHOT.jar SpringBootApp.jar

# Java start up options
# Listen on port 8000 for remote debugging
ENV JAVA_OPTS="-Xdebug -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n -Djava.security.egd=file:/dev/./urandom"

# Expose port 8080 for production
EXPOSE 8080
EXPOSE 8000

# Run Jar package when container launches
ENTRYPOINT exec java ${JAVA_OPTS} -jar SpringBootApp.jar --spring.config.location=application.yml