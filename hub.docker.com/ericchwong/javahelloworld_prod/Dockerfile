FROM java:7

RUN apt-get install -y curl
COPY HelloWorld.java /home/root/javahelloworld/src/
RUN ls -l /home/root/javahelloworld/src
#COPY src /home/root/javahelloworld/src

WORKDIR /home/root/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java

ENV JAVA_HOME /usr/bin/java
ENV APP_PORT 8080

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
