From java:7
MAINTAINER Docker Training <education@docker.com>

WORKDIR /home/root/javahelloworld
RUN mkdir bin

ADD src /home/root/javahelloworld/src
#COPY src /home/root/javahelloworld/src
RUN javac -d bin src/HelloWorld.java

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
RUN apt-get install -y wget
ENV FOO bar
