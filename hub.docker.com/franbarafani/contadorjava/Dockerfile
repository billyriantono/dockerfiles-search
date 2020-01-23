#-------------------------------------------------
# Stage 1 - Construyo el binario
#-------------------------------------------------
FROM ubuntu:16.04 as builder
LABEL maintainer="workshop2018" \
      version="0.0.1" \
      stage="build" \
      description="Basic example to test multistage build"

RUN apt-get update && \
    apt-get install -y default-jdk && \
    mkdir /app

WORKDIR /app
COPY main.java /app
RUN javac main.java

#-------------------------------------------------
# Stage 2 - Ejecuto el binario
#-------------------------------------------------
FROM openjdk:8-jre-alpine
LABEL maintainer="workshop2018" \
      version="0.0.1" \
      stage="execute" \
      description="Basic example to test multistage build"

RUN apk update

COPY --from=builder /app/. /bin/app
WORKDIR /bin/app
ENTRYPOINT java program
