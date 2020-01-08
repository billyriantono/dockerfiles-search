FROM alpine:latest

RUN apk --update add openjdk8-jre

ADD HelloWorld.class HelloWorld.class

ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "HelloWorld"]
