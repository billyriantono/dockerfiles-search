FROM java:7
MAINTAINER Whizzo Leopardprint <whizzo@leopardprint.com>

ENV FOO bar

COPY src /home/root/javahelloworld/src
WORKDIR /home/root/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN apt-get update && apt-get -y install vim

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]

# Inconsequential Commit
