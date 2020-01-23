FROM openjdk:7
WORKDIR /home/root/javahelloworld
ENV FOO bar
COPY src /home/root/javahelloworld/src
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp" ,"bin" ,"HelloWorld"]
