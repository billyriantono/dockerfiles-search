FROM microsoft/aspnetcore

USER root

# install packages
RUN apt-get update && \
    apt-get install -y zip unzip nodejs
RUN update-alternatives --install /usr/bin/node node /usr/bin/nodejs 10

RUN mkdir -p /app
VOLUME /app
WORKDIR /app

EXPOSE 80
