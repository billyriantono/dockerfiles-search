
FROM node:dubnium
WORKDIR /app
ENV DATABASE_URL=postgres://password@localhost:5432/psdb
COPY package*.json ./
RUN yarn global add node-gyp && yarn install
COPY . /app
EXPOSE 8080
CMD [ "node","server.js" ]
