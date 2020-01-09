FROM openjdk:8
ADD target/medicare-service-0.0.1-SNAPSHOT.jar medicare-service-0.0.1-SNAPSHOT.jar
EXPOSE 8061
ENTRYPOINT [ "java" , "-jar" , "-Dserver.port=8061","medicare-service-0.0.1-SNAPSHOT.jar" ]
