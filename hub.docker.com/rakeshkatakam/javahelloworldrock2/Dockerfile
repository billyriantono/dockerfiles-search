FROM java:6
WORKDIR src
COPY src/HelloWorld.java /
RUN javac src/HelloWorld.java
ENTRYPOINT ["java","HelloWorld"]
