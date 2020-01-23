FROM java:7

# base dir
WORKDIR /opt/javahelloworld

COPY src /opt/javahelloworld/src
#COPY bin /opt/javahelloworld/bin
RUN mkdir bin

RUN javac -d ./bin ./src/HelloWorld.java
RUN mkdir images

ENTRYPOINT ["java","-cp","bin","HelloWorld"]
