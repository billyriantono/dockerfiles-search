FROM node:8-alpine

# ENV NODE_VERSION 8.12.0

WORKDIR /src/app

COPY package.json /src/app
RUN npm install

COPY . /src/app

CMD ["npm","start"]

EXPOSE 3000