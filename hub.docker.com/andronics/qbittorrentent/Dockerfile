FROM node:latest
LABEL maintainer="Andre Nascimento"
COPY . /code
WORKDIR /code/server
RUN npm install
ENTRYPOINT ["node", "server.js"]