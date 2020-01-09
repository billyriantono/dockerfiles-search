FROM node:8-alpine
RUN mkdir -p ./docker/src/app
WORKDIR ./docker/src/app
COPY . .
RUN npm install
EXPOSE 3000
CMD [ "node", "server.js" ]
