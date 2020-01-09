# Start with a base image containing Java runtime
FROM hirokimatsumoto/alpine-openjdk-11:latest

# Add Maintainer Info
LABEL maintainer="fernando_lomonaco@outlook.com"

# Add a volume pointing to /tmp
VOLUME /tmp

# Make port 8080 available to the world outside this container
EXPOSE 8080

# Environment
ENV profile prod

# The application's jar file
ARG JAR_FILE

# Add the application's jar to the container
ADD ${JAR_FILE} monacosb.jar

# Run the jar file
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/monacosb.jar", "--spring.config.location=file:///config/${profile}/application.properties"]
