FROM node:alpine

ARG arch=arm64
ENV ARCH=arm64

RUN apk --no-cache add git

ENV FILE main.js  # Change the file to start

WORKDIR /node

CMD npm install && node /node/${FILE}
