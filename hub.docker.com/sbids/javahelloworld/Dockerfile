FROM java:8
RUN mkdir src
#RUN mkdir bin
COPY src/* /src/
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "HelloWorld"]
