FROM node:10.15.3
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . .
CMD node index.js
EXPOSE 8081