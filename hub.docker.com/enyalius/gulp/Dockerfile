FROM alpine:3.6
MAINTAINER Marcio Bigolin <marcio.bigolinn@gmail.com>
LABEL Description="Imagem do GULP!"

RUN apk --update add yarn


RUN mkdir /app
RUN yarn global add gulp
WORKDIR /app
