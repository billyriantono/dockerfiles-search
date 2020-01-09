FROM java:9

COPY src /home/root/hello/src

WORKDIR /home/root/hello

RUN mkdir bin && javac -d bin src/HelloWorld.java

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
