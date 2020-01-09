FROM java:8
COPY src /home/root/javahelloworld/src
WORKDIR /home/root/javahelloworld
RUN mkdir bin && javac -d bin src/HelloWorld.java
ENV FOO bar
RUN apt-get -y update && apt-get install -y nodejs
ENTRYPOINT ["java", "-cp", "bin","HelloWorld"]
