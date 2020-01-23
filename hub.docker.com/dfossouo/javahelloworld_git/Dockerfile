FROM anapsix/alpine-java:7_jdk
COPY src /home/root/javahelloworld/src
#RUN javac HelloWorld.java
WORKDIR /home/root/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java","-cp","bin","HelloWorld"]
ENV FOO bar
