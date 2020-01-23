FROM java:7

COPY src/HelloWorld.java /home/root/javahelloworld/

ENV FOO bar

WORKDIR /home/root/javahelloworld

RUN mkdir bin
RUN pwd 
RUN javac -d bin HelloWorld.java

ENTRYPOINT ["java","-cp","bin","HelloWorld"]


