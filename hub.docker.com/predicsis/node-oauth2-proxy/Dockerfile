FROM quay.io/predicsis/nodejs
MAINTAINER wnkz

ADD / /nodejs
WORKDIR /nodejs
RUN npm install

EXPOSE 8001

CMD node proxy.js
