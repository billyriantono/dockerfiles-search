FROM java:8
WORKDIR /home/root/javahelloworld
RUN mkdir bin
COPY src /home/root/javahelloworld/src
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]

