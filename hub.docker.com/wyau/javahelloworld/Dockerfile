FROM java:7
MAINTAINER wyau
ADD src.tar /home/root/javahelloworld
COPY src.tar /home/root/javahelloworld
WORKDIR /home/root/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN apt-get update
RUN apt-get install -y nginx
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
ENV FOO bar
