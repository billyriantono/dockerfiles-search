FROM node:10-alpine
ENTRYPOINT ["node", "server.js"]
WORKDIR /opt/basic-auth-proxy
COPY package.json .
RUN npm install
COPY server.js .
