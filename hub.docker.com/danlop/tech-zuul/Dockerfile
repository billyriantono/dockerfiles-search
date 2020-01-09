FROM openjdk:8-jdk-alpine

VOLUME /tmp

EXPOSE 8765

COPY ./target/tech-zuul-0.0.1-SNAPSHOT.jar tech-zuul.jar

ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "-Dspring.profiles.active=docker", "-jar", "/tech-zuul.jar"]