FROM java:7
WORKDIR /home/root
RUN mkdir bin
COPY src/HelloWorld.java src/
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
