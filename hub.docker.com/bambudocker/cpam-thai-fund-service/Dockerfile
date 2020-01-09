FROM node:10.14.1-alpine

RUN apk update && apk upgrade
RUN apk add --update tzdata

RUN rm -rf /var/cache/apk/*

WORKDIR /app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
# test
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm install --only=production

# Bundle app source
COPY . .

EXPOSE 3000
CMD [ "npm", "start" ]