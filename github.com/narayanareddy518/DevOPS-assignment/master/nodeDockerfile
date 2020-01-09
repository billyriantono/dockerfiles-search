FROM node:10
WORKDIR /index
COPY package*.json ./
RUN npm install
COPY . /index
CMD node app.js
EXPOSE 8888

