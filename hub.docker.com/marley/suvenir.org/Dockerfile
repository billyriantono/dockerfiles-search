FROM node:alpine

RUN apk update && apk upgrade && \
  apk add --no-cache bash git 

WORKDIR '/project'

COPY ./package*.json .
RUN npm install

COPY . .

CMD ["npm", "run", "start"]