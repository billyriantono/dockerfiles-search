FROM java:7
#COPY HelloWorld.java /
RUN apt-get install -y wget
COPY src /home/root/javahelloworld/src
WORKDIR /home/root/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
ENV FOO bar
