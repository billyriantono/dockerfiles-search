FROM node:10.9

WORKDIR /usr/src/app
COPY package*.json ./

RUN apt-get install libkrb5-dev
RUN npm install

COPY . .
EXPOSE 9000
CMD [ "npm", "run", "server"  ]



