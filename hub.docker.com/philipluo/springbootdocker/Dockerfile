FROM maven:3.5-jdk-8-alpine as build
WORKDIR /app
ADD / /app
RUN mvn install -Dmaven.test.skip=true

FROM openjdk:8-slim
WORKDIR /app
COPY --from=build /app/target/philipl-springboot-docker.jar /app
EXPOSE 8080
CMD ["java","-jar","philipl-springboot-docker.jar"]