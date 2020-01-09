FROM java:7
COPY src /home/root/javahw/src
WORKDIR /home/root/javahw
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]

