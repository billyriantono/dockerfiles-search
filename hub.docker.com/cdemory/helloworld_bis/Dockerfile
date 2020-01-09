FROM java:7
MAINTAINER Docker training hello
COPY src /home/root/javahelloworld/src
WORKDIR /home/root/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENV FOO bar
ENTRYPOINT ["java","-cp","bin","HelloWorld"]
