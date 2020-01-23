# From https://blog.xebialabs.com/2017/05/25/multi-stage-docker-image-build-for-java-applications/
FROM openjdk:8 AS BUILD_IMAGE
ENV APP_HOME=/root/dev/coupon/
WORKDIR $APP_HOME

COPY build.gradle gradlew gradlew.bat gradle.properties settings.gradle $APP_HOME
COPY gradle $APP_HOME/gradle
RUN ./gradlew clean build  --continue

COPY ./src/main ./src/main
RUN ./gradlew build

CMD ["java", "-jar", "build/libs/code-review-1.0-SNAPSHOT.jar"]