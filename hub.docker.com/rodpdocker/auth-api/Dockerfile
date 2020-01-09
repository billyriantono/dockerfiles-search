FROM node:alpine

WORKDIR /

COPY package*.json ./

RUN npm install --only=prod

COPY . .

EXPOSE 1986

CMD ["npm", "start"]