FROM java:7

COPY src /home/student/javahelloworld/src
WORKDIR /home/student/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN apt-get update && apt-get install -y vim
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
