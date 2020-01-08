FROM openjdk:8-slim

RUN apt-get update

RUN apt-get install -y curl git

RUN curl -sL https://deb.nodesource.com/setup_11.x | bash -
RUN apt-get install -y nodejs

EXPOSE 3000 3001