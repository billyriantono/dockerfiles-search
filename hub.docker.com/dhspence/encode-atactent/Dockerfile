FROM java:7
COPY HelloWorld.java /
RUN apt-get update && apt-get install -y vim
RUN javac HelloWorld.java
ENTRYPOINT ["java", "HelloWorld"]
