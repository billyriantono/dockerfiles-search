FROM java:7

COPY src /src
RUN apt-get install -y wget
RUN javac -d bin src/HelloWorld.java

ENTRYPOINT ["java","-cp","bin", "HelloWorld"]
