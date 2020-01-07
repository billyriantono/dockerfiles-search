FROM java:7

MAINTAINER Vincent RAVERA <ravera.vincent@gmail.com>

WORKDIR /home/root/javahelloworld
COPY src /home/root/javahelloworld/src
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN apt-get update
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
