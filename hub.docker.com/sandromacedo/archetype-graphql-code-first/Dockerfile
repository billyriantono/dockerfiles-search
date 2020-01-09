FROM node:11

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install ts-node --save-dev
RUN npm install typescript -g 
RUN npm install typescript --save-dev
RUN npm install

COPY . .

EXPOSE 4000
CMD [ "npm", "start" ]