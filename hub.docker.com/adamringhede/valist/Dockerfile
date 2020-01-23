FROM gradle:6.0-jdk11 as builder

COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle clean build -x test

FROM gradle:6.0-jdk11

EXPOSE 8080

COPY --from=builder /home/gradle/src/build/distributions/valist-host.zip /app/
WORKDIR /app
RUN apt update && apt install net-tools
RUN unzip valist-host.zip
COPY keystore.jks /app/keystore.jks

ENTRYPOINT valist-host/bin/valist-host