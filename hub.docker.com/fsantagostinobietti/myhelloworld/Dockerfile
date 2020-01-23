FROM java:7

COPY src /home/root/javahelloworld/src
WORKDIR /home/root/javahelloworld

RUN mkdir bin && javac -d bin src/HelloWorld.java
RUN echo "..."

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]


