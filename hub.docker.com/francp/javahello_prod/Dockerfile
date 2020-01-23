FROM java:7
COPY HelloWorld.java /
RUN apt-get -y install curl
RUN javac HelloWorld.java
ENTRYPOINT ["java", "HelloWorld"]
