FROM node:10
WORKDIR /usr/src/app
COPY ./dist .
RUN npm install
EXPOSE 80
CMD ["node", "server.js"]
