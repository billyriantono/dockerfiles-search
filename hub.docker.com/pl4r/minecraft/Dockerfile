FROM arm64v8/alpine:latest
MAINTAINER David McElin
COPY qemu-aarch64-static /usr/bin/
RUN apk add openjdk8-jre-base
WORKDIR /repo/Minecraft
ENTRYPOINT ["java", "-Xmx1024M", "-Xms1024M", "-jar", "/repo/Minecraft/server.jar"]
