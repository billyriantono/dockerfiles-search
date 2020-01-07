FROM node:alpine

WORKDIR /app

COPY $PWD .

RUN npm install

EXPOSE 4200

CMD [ "npm", "start", "--prod"]