FROM node:alpine

WORKDIR /check-mixed-content

COPY package.json .

RUN npm install

COPY src/ .

ENTRYPOINT [ "node", "index.js" ]