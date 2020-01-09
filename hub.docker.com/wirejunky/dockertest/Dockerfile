FROM node:8.5.0-alpine

RUN apk update && apk upgrade && \
        apk add --no-cache bash git openssh

WORKDIR /usr/src/app

COPY package.json package-lock.json ./

RUN npm install

COPY . .

EXPOSE 8080

CMD ["npm", "start"]
