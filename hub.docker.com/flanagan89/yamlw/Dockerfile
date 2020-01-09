FROM node:lts-alpine

WORKDIR /yamlw
COPY package.json .
COPY package-lock.json .

RUN npm install
COPY . .

WORKDIR /host
ENTRYPOINT ["node", "/yamlw/index.js"]