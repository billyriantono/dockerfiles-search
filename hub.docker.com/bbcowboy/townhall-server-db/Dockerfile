FROM node:8

WORKDIR /app

COPY package.json package.json

RUN npm install

COPY . .

RUN npm run build
