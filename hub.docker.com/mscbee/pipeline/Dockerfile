FROM openjdk:8u111-jdk-alpine
VOLUME /tmp
ADD /classes/artifacts/pipeline_jar/pipeline.jar app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
