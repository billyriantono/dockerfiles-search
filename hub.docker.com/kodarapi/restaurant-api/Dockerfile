FROM gradle:4.7.0-jdk8-alpine AS build
COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle build -x test

FROM openjdk:8-jre-alpine
COPY --from=build /home/gradle/src/build/libs/restaurant-api-ci-0.0.1-SNAPSHOT.jar /usr/src/restaurant-api/restaurant-api-ci-0.0.1-SNAPSHOT.jar
WORKDIR /usr/src/restaurant-api
EXPOSE 8080
CMD ["java", "-jar", "restaurant-api-ci-0.0.1-SNAPSHOT.jar"]
