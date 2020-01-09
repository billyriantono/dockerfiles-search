FROM java:7
COPY src /root/day2/javahelloworld/src
WORKDIR /root/day2/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
