FROM gradle:jdk11 as builder
LABEL maintainer="Pitera <pitjakub@gmail.com>"

RUN git clone https://github.com/kubAretip/zadanie5_1.git

COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle build --no-daemon

FROM openjdk:11.0-jre-slim

EXPOSE 8080

RUN mkdir /app

COPY --from=builder /home/gradle/src/build/libs/*.jar /app/zadanie_5_1_app.jar

CMD ["java","-jar","/app/zadanie_5_1_app.jar"]