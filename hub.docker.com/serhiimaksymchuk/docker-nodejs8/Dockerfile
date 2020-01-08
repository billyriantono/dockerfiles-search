FROM docker:latest
MAINTAINER Serhii Maksymchuk <serg.maximchuk@gmail.com>

RUN apk add --update nodejs nodejs-npm

RUN node -v

RUN npm install -g n
RUN node -v
RUN npm install -g npm@latest
RUN npm -v

CMD [ "node" ]
