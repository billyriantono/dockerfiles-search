FROM openjdk:8-jdk-alpine

ADD src /project/src
ADD gradle /project/gradle
ADD build.gradle /project
ADD gradlew /project
ADD gradlew.bat /project
ADD settings.gradle /project

WORKDIR /project

ENTRYPOINT ["./gradlew", "bootrun"]
