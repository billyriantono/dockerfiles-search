FROM alpine:latest
ADD HelloWorld.class HelloWorld.class
#ADD HelloWorld.java HelloWorld.java
RUN apk --update add openjdk8-jre
#RUN javac HelloWorld.java
ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom", "HelloWorld"]

