FROM node:10-alpine
LABEL version=1.0.0
WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000
CMD ["node", "./bin/www"]
