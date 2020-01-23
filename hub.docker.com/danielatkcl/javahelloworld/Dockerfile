FROM java:7-alpine

WORKDIR /home/root/javahelloworld

RUN mkdir src
RUN mkdir bin

COPY src/HelloWorld.java src

ENV FOO bar

RUN javac -d bin src/HelloWorld.java

CMD ["java","-cp","bin","HelloWorld"]
