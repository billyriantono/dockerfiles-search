FROM openjdk:7-jdk
COPY src/HelloWorld.java /home/root/javahelloworld/src/HelloWorld.java
WORKDIR /home/root/javahelloworld
ENV FOO bar
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN apt-get update && apt-get install -y vim
ENTRYPOINT ["java", "-cp","bin" , "HelloWorld"]
