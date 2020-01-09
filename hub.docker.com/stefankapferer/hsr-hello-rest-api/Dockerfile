FROM maven:3.3.9-jdk-8

# Working directory
WORKDIR /api

# Add pom.xml and source
ADD pom.xml /api/pom.xml
ADD src /api/src

# Build the API
RUN ["mvn", "clean", "package"]

RUN bash -c 'touch /api/target/rest-api-1.0.0.jar'

ENTRYPOINT ["java", "-jar", "/api/target/rest-api-1.0.0.jar"]

