FROM node:9.6.1

RUN mkdir /usr/src/mynuch
WORKDIR /usr/src/mynuch

COPY package.json /usr/src/mynuch/
RUN npm install

COPY . /usr/src/mynuch

CMD ["npm","start"]

