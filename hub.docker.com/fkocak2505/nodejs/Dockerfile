FROM node:latest

MAINTAINER fkocak2505@gmail.com

RUN mkdir -p /src/nodeapp
WORKDIR /src/nodeapp

COPY package.json /src/nodeapp
RUN npm install
COPY . /src/nodeapp

EXPOSE 9393
CMD ["node", "server.js"]