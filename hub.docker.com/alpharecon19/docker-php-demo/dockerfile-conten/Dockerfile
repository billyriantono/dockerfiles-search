FROM java:8
#MAINTAINER bob <bob@nowhere.org>
ENV MVN_HOME /home/mvn
COPY src /home/root/javahelloworld/src
WORKDIR /home/root/javahelloworld
RUN mkdir -p bin
RUN javac -d bin src/HelloWorld.java
RUN apt-get install -y wget
ENTRYPOINT  [ "java", "-cp", "bin", "HelloWorld" ]

