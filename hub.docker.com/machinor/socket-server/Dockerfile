FROM node:11.1.0

WORKDIR /usr/src/app
COPY package.json ./
COPY yarn.lock ./
RUN yarn
COPY . .
EXPOSE 8081
CMD ["node", "server.js"]
