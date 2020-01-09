FROM ubuntu:18.04

LABEL maintainer="Stefano Baghino <stefano@baghino.me>"

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y git=1:2.17.1-1ubuntu0.1 openjdk-8-jdk=8u171-b11-0ubuntu0.18.04.1

RUN git clone -b v2.3b66 https://github.com/ether-camp/ethereum-harmony /ethereum-harmony

WORKDIR /ethereum-harmony

RUN ./gradlew compileJava

ENTRYPOINT ["./gradlew"]

CMD ["runMain"]