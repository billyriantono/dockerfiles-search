FROM node:0.12

WORKDIR /app
COPY package.json /app/package.json
RUN npm install
COPY . /app

EXPOSE 9092

CMD npm start
