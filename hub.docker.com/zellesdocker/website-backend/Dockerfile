FROM node:10

WORKDIR /app
COPY package*.json ./

RUN npm install

COPY . .

VOLUME /app/config

EXPOSE 9000
CMD [ "npm", "start" ]
