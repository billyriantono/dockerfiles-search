FROM openjdk:8
# Add Maintainer Info
LABEL maintainer="andrew.haman@yahoo.com"
# Make port 8080 available to the world outside this container
EXPOSE 8080
# Make fake fucking directory
RUN mkdir -p /app/
# Add the application's jar to the container
ADD ./docker/dece-0.0.1-SNAPSHOT.jar /app/dece-0.0.1-SNAPSHOT.jar
# Run the jar file
ENTRYPOINT ["java", "-jar", "/app/dece-0.0.1-SNAPSHOT.jar"]