FROM alpine
WORKDIR /hello-world
COPY src/main/java/Main.java /hello-world

RUN apk add openjdk8
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:$JAVA_HOME/bin

RUN javac Main.java

ENTRYPOINT java Main
