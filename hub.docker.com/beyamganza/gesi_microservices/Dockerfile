FROM node:8-slim

WORKDIR /server

COPY . /server
RUN npm install

EXPOSE 2222
CMD [ "npm", "start" ]
