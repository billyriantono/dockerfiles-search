FROM java:8
ENV FOO bar

WORKDIR /home/root/javahelloworld
RUN mkdir bin

COPY src /home/root/javahelloworld/src

RUN javac -d bin src/HelloWorld.java

RUN touch version1.1

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
