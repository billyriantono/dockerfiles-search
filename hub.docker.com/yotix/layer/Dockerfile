#This is a multi-stage Dockerfile and requires >= Docker 17.05
#https://docs.docker.com/engine/userguide/eng-image/multistage-build/
FROM openjdk:8 as builder
ENV APP_HOME=/usr/app/
WORKDIR $APP_HOME
COPY build.gradle settings.gradle gradlew $APP_HOME
COPY gradle $APP_HOME/gradle
RUN ./gradlew dependencies
COPY . .
RUN ./gradlew clean build


FROM openjdk:8
ENV ARTIFACT_NAME=server-0.0.1-SNAPSHOT.jar
ENV APP_HOME=/usr/app/
WORKDIR $APP_HOME
COPY --from=builder $APP_HOME/build/. $APP_HOME/build/.
# COPY build/. $APP_HOME/build/.
WORKDIR $APP_HOME/build/libs/
EXPOSE 5000
CMD ["java","-jar","server-0.0.1-SNAPSHOT.jar","--spring.profiles.active=prod"]
