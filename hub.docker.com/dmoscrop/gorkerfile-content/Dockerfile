FROM ubuntu:18.04

RUN apt-get update
RUN apt-get install -y git curl gnupg2

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update
RUN apt-get install -y nodejs yarn openjdk-11-jdk maven libgtk-3-0 libxss1 libasound2
