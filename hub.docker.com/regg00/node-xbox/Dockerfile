FROM node:alpine
LABEL maintainer="regis tremblay lefrancois"

RUN apk update && apk upgrade
RUN mkdir /app
COPY package.json /app
WORKDIR /app
RUN npm install
EXPOSE 80
COPY app.js /app
CMD ["npm", "start"]