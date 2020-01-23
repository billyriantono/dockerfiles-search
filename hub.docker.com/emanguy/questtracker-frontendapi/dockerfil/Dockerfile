FROM node:slim

LABEL mantainer="Eloy Lopez <elswork@gmail.com>"

RUN apt-get update && \
    apt-get install -y --no-install-recommends && \
    apt-get clean  

EXPOSE 8081

RUN mkdir -p my-app

VOLUME /root/my-app

WORKDIR /root/my-app

CMD bash