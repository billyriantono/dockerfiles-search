FROM node:10

WORKDIR ~/Documents/docker/real/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]