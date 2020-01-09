FROM java:7
RUN apt-get update
RUN apt-get -y install curl
COPY HelloWorld.java /
RUN javac HelloWorld.java
ENTRYPOINT ["java", "HelloWorld"]
