FROM java:7
COPY src /home/root/javahelloworld/src
WORKDIR /home/root/javahelloworld
ENV FOO bar
ENV TEST test1
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN mkdir lakshmi
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
