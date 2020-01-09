FROM java:7
COPY src /home/root/hello/src
WORKDIR /home/root/hello
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]