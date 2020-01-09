FROM java:7

WORKDIR /opt
MAINTAINER Pasquale Paola <pasquale.paola@gmail.com>
COPY HelloWorld.java /opt

RUN javac /opt/HelloWorld.java

#CMD java HelloWorld
ENTRYPOINT ["java","HelloWorld"]

