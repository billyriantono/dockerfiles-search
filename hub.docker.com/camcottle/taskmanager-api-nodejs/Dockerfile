FROM node:8.15.1-stretch

RUN mkdir -p /app

WORKDIR /app

COPY package.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
