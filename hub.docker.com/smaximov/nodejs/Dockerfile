FROM ubuntu:latest
MAINTAINER smaximov <s.b.maximov@gmail.com>

RUN apt-get update && apt-get install -y build-essential curl
    
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash -

RUN apt-get update && apt-get install -y nodejs

USER root
