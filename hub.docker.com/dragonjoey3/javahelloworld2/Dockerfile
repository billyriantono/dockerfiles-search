
FROM java:8

COPY src /home/root/helloworld/src
WORKDIR /home/root/helloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN apt-get update && apt-get install -y vim

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]

MAINTAINER Joe Furches <DragonJoey3@gmail.com>
