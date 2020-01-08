FROM node:slim
MAINTAINER Sean Huai <huaiyifan@live.com>

RUN npm install --quiet -g vue-cli
RUN mkdir /code

WORKDIR /code
RUN vue init webpack app 

WORKDIR /app
RUN npm install 

EXPOSE 8080
CMD npm run dev