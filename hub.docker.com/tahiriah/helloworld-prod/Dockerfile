FROM java:7
COPY src /usr/local/src/HelloWorld/src
WORKDIR /usr/local/src/HelloWorld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
