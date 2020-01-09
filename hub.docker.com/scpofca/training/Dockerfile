FROM java:7
MAINTAINER Francois en formation chez Alter Way
WORKDIR /root/javahelloworld
RUN mkdir bin
COPY src /root/javahelloworld/src
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
