FROM java:7
COPY src/HelloWorld.java /
ENV MYVAR ciao
RUN javac HelloWorld.java
RUN apt-get update && apt-get install -y vim && apt-get install -y curl
ENTRYPOINT ["java","HelloWorld"]


