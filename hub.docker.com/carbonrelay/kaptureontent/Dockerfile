FROM node:alpine

RUN apk update \
    && apk add aria2 git \
    && mkdir /g-uploader

COPY . /g-uploader

ENV USER admin
ENV PASSWORD google

WORKDIR /g-uploader

RUN npm install && chmod +x setup.sh

EXPOSE 3000

CMD ./setup.sh
