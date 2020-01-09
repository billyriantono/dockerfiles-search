FROM java:8

WORKDIR /home/root/javahelloworld

COPY src src

RUN mkdir bin && \
    javac -d bin src/HelloWorld.java && rm src/HelloWorld.java

ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
