FROM node:latest

EXPOSE 12345

COPY . /src

RUN cd /src; npm install

CMD["node", "/src/index.js"]