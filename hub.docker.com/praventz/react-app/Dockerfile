FROM node:alpine as builder
EXPOSE 3000
WORKDIR /app
COPY package*.json /app/
RUN npm install
COPY ./ /app/
RUN npm run build --prod
CMD npm start

