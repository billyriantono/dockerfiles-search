FROM java:7

WORKDIR /home/root/javahelloworld
RUN mkdir bin
ENV FOO bar

COPY src /home/root/javahelloworld/src
RUN javac -d bin src/HelloWorld.java
RUN touch /home/tempfile
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
