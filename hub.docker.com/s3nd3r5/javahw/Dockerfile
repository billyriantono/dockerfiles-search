FROM java:7

COPY src /home/root/javahw/src
WORKDIR /home/root/javahw

RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN apt-get update && apt-get install -y vim

ENTRYPOINT ["java","-cp","bin","HelloWorld"]
