FROM node:8.11.2-alpine

WORKDIR /app

COPY package*.json ./

RUN npm install
RUN npm install -g ionic

COPY . /app

EXPOSE 8100

CMD ["ionic",  "serve", "8100", "--address", "0.0.0.0"]