
FROM ubuntu:17.04

MAINTAINER Kaminchu <kmchu.mail@gmail.com>

#Let people know how this was built
ADD Dockerfile /root/Dockerfile

RUN apt-get update && \
    apt-get install -y git maven wget curl && \
    apt-get install -y openjdk-8-jre openjdk-8-jdk openjfx && \
    apt-get install -y nodejs npm

RUN npm cache clean && \
    npm install n -g && \
    n stable && \
    ln -sf /usr/local/bin/node /usr/bin/node