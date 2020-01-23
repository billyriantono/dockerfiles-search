FROM java:7
COPY src /home/java/src/
WORKDIR /home/java
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "Hello"]
