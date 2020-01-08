FROM node:7.10.0
MAINTAINER Yves Candel

RUN apt-get update && apt-get install -y --no-install-recommends \
    nginx

COPY ./nginx /etc/nginx

ADD package.json /tmp/package.json
RUN cd /tmp && npm install
RUN mkdir -p /build/app && cp -a /tmp/node_modules /build/app/

WORKDIR /build/app
ADD . /build/app

RUN npm run build

RUN rm -rf node_modules

WORKDIR ./dist

CMD ["nginx", "-g", "daemon off;"]