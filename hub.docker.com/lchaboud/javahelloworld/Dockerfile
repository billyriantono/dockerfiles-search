FROM java:7
ENV FOO bar
WORKDIR /home/root/javahelloworld
COPY src src

RUN mkdir bin && \
    javac -d bin src/HelloWorld.java
RUN echo $FOO

ENTRYPOINT java -cp bin HelloWorld
