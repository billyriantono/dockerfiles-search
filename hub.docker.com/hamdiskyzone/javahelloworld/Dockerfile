FROM java:8

COPY src /home/student/javahelloworld/src

WORKDIR /home/student/javahelloworld

RUN mkdir bin
RUN javac -d bin src/HelloWorld.java

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
