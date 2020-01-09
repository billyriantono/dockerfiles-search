FROM node:6
COPY /DSS2021/package.json /src/package.json

RUN  cd /src; npm install

COPY /DSS2021/. /src
EXPOSE 3000

WORKDIR /src
CMD node index.js

