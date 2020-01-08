FROM node:7-alpine

LABEL maintainer "Tiago Lopes da Costa <tiagolo@gmail.com>"

WORKDIR /app
COPY ./ /app
RUN npm install

EXPOSE 8080
CMD ["npm", "start"]
