FROM node:9.6.1

RUN mkdir /usr/src/myresume
WORKDIR /usr/src/myresume

COPY package.json /usr/src/myresume/
RUN npm install

COPY . /usr/src/myresume

CMD ["npm","start"]

