
FROM node:alpine
MAINTAINER Terry <2219569347@qq.com>

WORKDIR /app
COPY package.json .
RUN npm install --registry=https://registry.npm.taobao.org

COPY . /app
CMD ["npm","start"]

EXPOSE 3000