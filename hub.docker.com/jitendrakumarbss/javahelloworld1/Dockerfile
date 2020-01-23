FROM ubuntu:14.04
RUN apt-get update
RUN apt-get install -y wget
RUN apt-get install -y openjdk-7-jdk
WORKDIR /home/root/javahelloworld
COPY src /home/root/javahelloworld/src
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
