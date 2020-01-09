FROM java:7

#COPY HelloWorld.java /
COPY src /home/root/javahelloworld/src

WORKDIR /home/root/javahelloworld

#RUN javac HelloWorld.java
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java

ENV FOO bar

RUN touch readme.txt

#ENTRYPOINT ["java", "HelloWorld"]
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
