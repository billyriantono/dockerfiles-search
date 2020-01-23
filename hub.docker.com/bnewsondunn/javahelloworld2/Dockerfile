FROM java:8

COPY src /home/docker/testing/javahelloworld/src
WORKDIR /home/docker/testing/javahelloworld
ENV FOO bar 

RUN mkdir bin
RUN javac -d bin src/HelloWorld.java

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]

