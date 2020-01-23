FROM maven:3-jdk-8

MAINTAINER Chafik Hnini "chafik.hnini@gmail.com"

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && apt-get install -y nodejs

CMD mvn --version && node --version && npm --version
