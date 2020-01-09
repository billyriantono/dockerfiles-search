FROM java:7

WORKDIR /home/root/javahelloworld

COPY src /home/root/javahelloworld/src
COPY bin /home/root/javahelloworld/bin

RUN javac -d bin src/HelloWorld.java

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
