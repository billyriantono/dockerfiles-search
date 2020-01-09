FROM java:7

COPY src /home/root/javahelloworld/src
COPY bin /home/root/javahelloworld/bin

WORKDIR /home/root/javahelloworld

ENV FOO bar

RUN javac -d bin src/HelloWorld.java

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]

