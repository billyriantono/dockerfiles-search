FROM java:7
COPY  src /home/root/javahelloworld/src
RUN apt-get update
RUN apt-get install -y vim
WORKDIR /home/root/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java","-cp","bin","HelloWorld"]
ENV FOO bar
