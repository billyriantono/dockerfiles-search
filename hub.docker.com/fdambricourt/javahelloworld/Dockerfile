FROM java:7
WORKDIR /root/javahelloword
RUN mkdir bin
COPY src src
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin","HelloWorld"]
ENV FOO bar
