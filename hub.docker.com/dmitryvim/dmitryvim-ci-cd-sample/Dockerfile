# fix base image
FROM openjdk:8-slim AS build
ADD gradlew gradlew
ADD build.gradle build.gradle
ADD settings.gradle settings.gradle
ADD src/ src/
ADD gradle/ gradle/
RUN /gradlew build

# fix base image
FROM openjdk:8-slim
COPY --from=build /build/libs/dmitryvim-ci-cd-sample.jar /application.jar
ENTRYPOINT java -jar /application.jar