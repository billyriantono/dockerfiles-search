FROM java:7

MAINTAINER Guybrush Threepwood <antoine.ceol@zenika.com>

ENV FOO bar

EXPOSE 80 8080 

WORKDIR /home/root/javahelloworld
RUN mkdir /data/myvol -p
RUN echo "yosdfsdfyo yo" > /data/myvol/test
VOLUME /data/myvol
RUN mkdir bin src
RUN apt-get install -y git
COPY ./src ./src 
RUN ["javac","-d","bin","./src/Helloworld.java"]
