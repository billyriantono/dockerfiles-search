FROM node:12.13.0-alpine

WORKDIR /app

RUN npm install nodemon -g

COPY ["package.json", "package-lock.json*", "./"]

RUN npm install

COPY . .

EXPOSE 8080

CMD ["npm","start"]
