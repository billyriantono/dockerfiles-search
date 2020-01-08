FROM openjdk:8-jre
#FROM openjdk:8-jdk
#FROM onsdigital/java-component

ENV TZ Asia/Bangkok

#RUN apt-get clean

#WORKDIR /app

# Phantom.js
WORKDIR /usr/phantom
RUN apt-get install -y tar bzip2
COPY ./app/phantomjs-2.1.1-linux-x86_64.tar.bz2 /usr/phantom/phantom.tar.bz2
#or
#ADD https://github.com/Medium/phantomjs/releases/download/v2.1.1/phantomjs-2.1.1-linux-x86_64.tar.bz2 /usr/phantom/phantom.tar.bz2
RUN tar -xvjf phantom.tar.bz2
RUN mv phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin/
RUN rm /usr/phantom/phantom.tar.bz2
