FROM node:alpine

RUN mkdir -p /src/app
WORKDIR /src/app

RUN apk add tzdata --update --no-cache && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" /etc/localtime && apk del tzdata

COPY ./package.json package.json
# RUN npm config set registry https://registry.npm.taobao.org/
RUN npm i --production && npm cache clean -f

COPY ./. .
CMD npm start

EXPOSE 80
