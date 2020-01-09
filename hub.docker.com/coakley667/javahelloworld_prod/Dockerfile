FROM java:7
MAINTAINER Chris
ENV FOO bar
COPY src /home/root/javahelloworld/src
WORKDIR /home/root/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
#RUN apt-get -y update && apt-get -y install bb
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld" ]
