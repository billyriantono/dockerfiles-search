

# Nodejs_restart

#daocloud.io/

# VERSION    1.0.0

FROM node:5
MAINTAINER WSW@xyz9836@126.com

ENV HTTP_PORT 4000

COPY . /app
WORKDIR /app


RUN npm --registry=https://registry.npm.taobao.org --disturl=https://npm.taobao.org/dist install


EXPOSE 4000


CMD ["npm", "start"]
